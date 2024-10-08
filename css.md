Sure! Here's a **basic CSS cheat sheet** that covers fundamental CSS concepts, properties, and examples. This will help you quickly style your web pages during an exam or project.

---

## **CSS Cheat Sheet**

### 1. **Basic CSS Syntax**
```css
selector {
    property: value;
}
```
- **Selector**: Targets the HTML element(s) to style.
- **Property**: The CSS property you want to change (e.g., `color`, `font-size`).
- **Value**: The value of the property (e.g., `red`, `16px`).

### 2. **CSS Selectors**
- **Element Selector**: Targets all elements of a type.
  ```css
  p {
      color: blue;
  }
  ```
- **Class Selector**: Targets elements with a specific class.
  ```css
  .classname {
      color: green;
  }
  ```
  In HTML:
  ```html
  <p class="classname">This is a paragraph.</p>
  ```
- **ID Selector**: Targets a specific element with an ID.
  ```css
  #unique-id {
      font-size: 18px;
  }
  ```
  In HTML:
  ```html
  <div id="unique-id">This is a div.</div>
  ```

### 3. **Text Styling**
```css
p {
    color: #333;          /* Text color */
    font-size: 16px;       /* Font size */
    font-family: Arial, sans-serif;  /* Font family */
    text-align: center;    /* Center-align text */
    font-weight: bold;     /* Make text bold */
    text-decoration: underline;  /* Underline text */
}
```

### 4. **Background Styling**
```css
body {
    background-color: #f0f0f0;  /* Background color */
    background-image: url('image.jpg');  /* Background image */
    background-repeat: no-repeat;  /* Prevent repeating */
    background-size: cover;  /* Cover entire background */
}
```

### 5. **Box Model**
- The box model controls how padding, borders, and margins are applied to elements.
```css
div {
    width: 300px;           /* Element width */
    height: 200px;          /* Element height */
    padding: 20px;          /* Space inside the element */
    margin: 10px;           /* Space outside the element */
    border: 1px solid #ccc; /* Border around the element */
}
```

### 6. **Positioning Elements**
- **Static (default)**: Elements are positioned according to the normal document flow.
- **Relative**: Positioned relative to its normal position.
- **Absolute**: Positioned relative to the nearest positioned ancestor.
- **Fixed**: Positioned relative to the viewport (i.e., the window).

```css
div {
    position: relative;   /* Position relative to its normal position */
    top: 10px;            /* Move down by 10px */
    left: 20px;           /* Move right by 20px */
}
```

### 7. **Flexbox Layout**
Flexbox makes it easier to design flexible and responsive layouts.
```css
.container {
    display: flex;                /* Enable flexbox */
    justify-content: center;      /* Center horizontally */
    align-items: center;          /* Center vertically */
    flex-direction: row;          /* Arrange children in a row */
    gap: 10px;                    /* Space between flex items */
}
```

In HTML:
```html
<div class="container">
    <div>Item 1</div>
    <div>Item 2</div>
    <div>Item 3</div>
</div>
```

### 8. **CSS Grid Layout**
Grid is a powerful layout system for creating complex, responsive designs.
```css
.container {
    display: grid;
    grid-template-columns: 1fr 1fr 1fr;  /* Three equal columns */
    grid-gap: 10px;  /* Space between grid items */
}
```

In HTML:
```html
<div class="container">
    <div>Item 1</div>
    <div>Item 2</div>
    <div>Item 3</div>
</div>
```

### 9. **Hover and Active States**
```css
a:hover {
    color: red;             /* Change color when hovered */
}

button:active {
    background-color: green; /* Change background when clicked */
}
```

### 10. **Media Queries** (Responsive Design)
Use media queries to apply different styles for different screen sizes (e.g., mobile, tablet, desktop).
```css
/* For screens smaller than 600px */
@media only screen and (max-width: 600px) {
    body {
        font-size: 14px;
    }
    .container {
        flex-direction: column;  /* Stack elements vertically */
    }
}
```

### 11. **Centering Elements**
- **Horizontally center block-level elements**:
  ```css
  div {
      margin: 0 auto;
      width: 50%;
  }
  ```
- **Horizontally & vertically center with Flexbox**:
  ```css
  .center {
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;  /* Full viewport height */
  }
  ```

### 12. **CSS Colors**
- **Hexadecimal**: `#ff0000` (red)
- **RGB**: `rgb(255, 0, 0)` (red)
- **RGBA** (with transparency): `rgba(255, 0, 0, 0.5)`
- **Named colors**: `red`, `blue`, `green`, etc.

### 13. **Borders, Padding, and Margins**
```css
div {
    border: 2px solid black;   /* Solid black border */
    padding: 20px;             /* Space inside the element */
    margin: 10px;              /* Space outside the element */
}
```

### 14. **Z-Index (Stacking Elements)**
Used to control the vertical stacking order of elements (higher `z-index` appears on top).
```css
div {
    position: absolute;
    z-index: 10;
}
```

### 15. **Fonts and Typography**
```css
body {
    font-family: Arial, sans-serif;  /* Font family */
    font-size: 16px;                 /* Font size */
    font-weight: bold;               /* Font weight */
    line-height: 1.5;                /* Line height */
    letter-spacing: 1px;             /* Letter spacing */
}
```

### 16. **Buttons Styling**
```css
button {
    background-color: #4CAF50; /* Green background */
    color: white;              /* White text */
    padding: 10px 20px;        /* Padding inside button */
    border: none;              /* Remove border */
    cursor: pointer;           /* Pointer cursor on hover */
}

button:hover {
    background-color: #45a049; /* Darker green on hover */
}
```

### 17. **Links Styling**
```css
a {
    color: blue;            /* Link color */
    text-decoration: none;  /* Remove underline */
}

a:hover {
    color: red;             /* Change color on hover */
}
```

---

### **Quick References:**

- **Units**:
  - `px`: Pixels
  - `%`: Percentage
  - `em`, `rem`: Relative to font size (1em = current font size, 1rem = root font size)
  - `vh`, `vw`: Viewport height/width

- **Box Shadow**:
  ```css
  div {
      box-shadow: 5px 5px 10px #888888;  /* X-offset, Y-offset, blur radius, color */
  }
  ```

- **Transitions** (for animations):
  ```css
  div {
      transition: all 0.3s ease-in-out;  /* Applies transition to all properties */
  }

  div:hover {
      background-color: red;  /* Change on hover */
  }
  ```

- **Opacity**:
  ```css
  img {
      opacity: 0.7;  /* 70% opacity */
  }
  ```

---

### **Useful Resources**:
- [CSS Tricks](https://css-tricks.com/)
- [MDN Web Docs: CSS](https://developer.mozilla.org/en-US/docs/Web/CSS)
- [W3Schools: CSS](https://www.w3schools.com/css/)

---

This cheat sheet provides a quick reference to fundamental CSS properties and techniques, including selectors, layout systems, and responsive design techniques (media queries). This should cover most of the basic styles you'll need for an exam! Let me know if you'd like additional topics included.