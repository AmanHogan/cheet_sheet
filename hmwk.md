# Homework 1
```js

function getQueryString() {
   var formattedTermValue = document.getElementById("term").value.trim().toLowerCase().replace(/[\s,]+/g, '+');
   var formattedCityValue = document.getElementById("city").value.trim().toLowerCase().replace(/[\s,]+/g, '+');
   var levelLimitValue = document.getElementById("level").value;
   var queryString = "proxy.php?term=" + formattedTermValue + "&location=" + formattedCityValue + "&limit=" + levelLimitValue;
   return queryString
}

function findRestaurants () {
    var xhr = new XMLHttpRequest();
    const qString = getQueryString(); 
   
    // Call yelp api
    xhr.open("GET", qString);
    xhr.setRequestHeader("Accept","application/json");
    xhr.onreadystatechange = function () {
        if (this.readyState == 4) {
            var json = JSON.parse(this.responseText);

            if (json.businesses && json.businesses.length > 0) {
                console.log(json.businesses);
                displayResults(json.businesses);
            }

            else{
                let outputDiv = document.getElementById('output');
                outputDiv.innerHTML = '<p>No businesses found for the given query.</p>';
            }
        }
    };
    xhr.send(null);
}

async function displayResults(businesses) {
   // Clear previous results
   let outputDiv = document.getElementById('output');
   outputDiv.innerHTML = '';

   	// Create ordered list
	const orderedList = document.createElement('ol');
	orderedList.style.paddingLeft = '20px'; 
   
	// Sort by rating (best business is 1)
	businesses.sort((a, b) => b.rating - a.rating);

	// Limit results to top 10 or less if less than 10 results
	const numResults = Math.min(businesses.length, 10);

	for (let i = 0; i < numResults; i++) {
		let business = businesses[i];

		// Create list item
		const listItem = document.createElement('li');
		listItem.style.marginBottom = '20px';

		// Create a card
		let card = document.createElement('div');
		card.style.border = "solid";
		card.style.padding = "15px";
		card.style.margin = "10px 50px 0px";
		card.style.boxShadow = "0 4px 8px 0 rgba(0, 0, 0, 0.1)";

		// Details container
		const details = document.createElement('div');
		details.style.flex = '1';
		
		// Add rank 
		let rankingText = document.createElement('h2');
		rankingText.innerHTML = `Match: ${i+1}`;
		card.appendChild(rankingText);

		// Image
		let img = document.createElement('img');
		img.src = business.image_url;
		img.alt = `${business.name} image`;
		img.style.width = "100px";
		card.appendChild(img);
		
		// Name and Link
		let nameLink = document.createElement('a');
		nameLink.href = business.url;
		nameLink.target = "_blank";
		nameLink.innerHTML = business.name;
		nameLink.style.display = "block";
		card.appendChild(nameLink);
		
		// Categories
		let categories = business.categories.map(cat => cat.title).join(', ');
		let categoriesText = document.createElement('p');
		categoriesText.innerHTML = `Categories: ${categories}`;
		card.appendChild(categoriesText);
		
		// Price, Price sometimes isn't included for some reason
		if (business.price) 
		{
			let priceText = document.createElement('p');
			priceText.innerHTML = `Price: ${business.price}`;
			card.appendChild(priceText);
		}
		
		// Rating
		let ratingText = document.createElement('p');
		ratingText.innerHTML = `Rating: ${business.rating} / 5`;
		card.appendChild(ratingText);
		
		// Address, formatted
		let addressText = document.createElement('p');
		addressText.innerHTML = `Address: ${business.location.address1}, ${business.location.city}, ${business.location.zip_code}`;
		card.appendChild(addressText);
		
		// Phone number
		let phoneText = document.createElement('p');
		phoneText.innerHTML = `Phone: ${business.display_phone}`;
		card.appendChild(phoneText);

		// Append details to card
		card.appendChild(details);
		listItem.appendChild(card);
		orderedList.appendChild(listItem);
	}

	outputDiv.appendChild(orderedList);
}

```
# Homework 2


```js

let map; // Google Map
let markers = []; // Google Map Markers
let infoWindow; // Popup Window
let currentSearchTerm = ''; // Search term in search bar at given moment

DEFAULT_LAT = 32.75
DEFAULT_LNG = -97.13
DEFAULT_ZOOM = 16

function initMap() 
{
	map = new google.maps.Map
	(document.getElementById('map'), 
		{
		center: { lat: DEFAULT_LAT, lng: DEFAULT_LNG },
		zoom: DEFAULT_ZOOM = 16
		}
	);

	// Initialize the popup information window
	infoWindow = new google.maps.InfoWindow();

	//  Update map, when it is moved or zoomed
	map.addListener
	('idle', function() 
		{
		findRestaurants();
		}
	);
}


/**
 * Ensures yelp only searches on the displayed map
 * @returns lat,long,radius
 */
function getMapBounds() 
{
	const bounds = map.getBounds();
	const center = bounds.getCenter();
	const ne = bounds.getNorthEast();
	const radius = google.maps.geometry.spherical.computeDistanceBetween(center, ne);
	const radiusInMeters = Math.min(Math.round(radius), 40000); // Round the radius to the nearest integer

	var mapBounds = 
	{
		latitude: center.lat(),
		longitude: center.lng(),
		radius: radiusInMeters
	};

	return mapBounds;
}


function getQueryString() {

	const searchTermInput = document.getElementById("term").value.trim().toLowerCase();

	if (searchTermInput) {
		currentSearchTerm = searchTermInput; 
	}

	if (!currentSearchTerm) {
		return '';
	}

	const formattedTermValue = currentSearchTerm.replace(/[\s,]+/g, '+');
	const bounds = getMapBounds();
	return `proxy.php?term=${formattedTermValue}&latitude=${bounds.latitude}&longitude=${bounds.longitude}&radius=${bounds.radius}&limit=10`;
}


function findRestaurants(){
	const qString = getQueryString();
	if (!qString) {
		console.log('No search term, skipping search.');
		return;
	}

	clearMarkers();
	
	// Call Yelp API
	const xhr = new XMLHttpRequest();
	xhr.open("GET", qString);
	xhr.setRequestHeader("Accept", "application/json");
	xhr.onreadystatechange = function () {
		if (this.readyState == 4) {
			const json = JSON.parse(this.responseText);
			console.log(json);
			if (json.businesses && json.businesses.length > 0) {
				displayResults(json.businesses);	
			} 
			else {
				console.log('No businesses found');
			}
		}
	};
	xhr.send(null);
}


function clearMarkers() {
	for (let marker of markers) {
		marker.setMap(null);
	}
	markers = [];
}

function displayResults(businesses) {
	let outputDiv = document.getElementById('output');
	outputDiv.innerHTML = '';

	businesses.sort((a, b) => b.rating - a.rating);
	
	for (let i = 0; i < businesses.length; i++) {
		// Create new marker
		let business = businesses[i];
		let marker = new google.maps.Marker
		(
			{
				position:
				{
					lat: business.coordinates.latitude,
					lng: business.coordinates.longitude
				},
				label: `${i + 1}`,
				map: map
			}
		);

		// Event listener to the marker to display an info window when marker is clicked
		google.maps.event.addListener
		(marker, 'click', function() 
			{
				infoWindow.setContent(`
					<div>
					<h2>${business.name}</h2>
					<img src="${business.image_url}" style="width:100px;" alt="${business.name}">
					<p>Rating: ${business.rating} / 5</p>
					<p>${business.location.address1}, ${business.location.city}</p>
					</div>
				`);
				infoWindow.open(map, marker);
			}
		);
		markers.push(marker);
  	}
}

```