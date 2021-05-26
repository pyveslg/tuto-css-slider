## Objective

Design a mobile-friendly css-only slider

## Approach

I used css-grid but this could be achieved as well with flexboxes.

## Comments of my code

### **1. Prepare your HTML structure**
Draw it with excalidraw

### **2. Create your card component**
HTML
```html
  <div class="card-category" style="background-image: linear-gradient(rgba(0,0,0,0.3), rgba(0,0,0,0.3)), url(https://images.unsplash.com/photo-1574963835057-bcc8418c971c?ixlib=rb-1.2.1&ixid=MXwxMjA3fDB8MHxleHBsb3JlLWZlZWR8MTMwfHx8ZW58MHx8fA%3D%3D&auto=format&fit=crop&w=800&q=60)">
    Golden Apples
  </div>
```
and then css
```css
  .card-category {
    background-size: cover;
    background-position: center;
    height: 180px;
    display: flex;
    justify-content: center;
    align-items: center;
    color: white;
    font-size: 24px;
    font-weight: bold;
    text-shadow: 1px 1px 3px rgba(0,0,0,0.2);
    border-radius: 5px;
    box-shadow: 0 0 15px rgba(0,0,0,0.2);
    text-align: center;
  }
```

### **3. Define slider behavior**

no margin on right except once at the end of carousel
no bounce effect at the end of the slider

### **4. Code slider**

  **1. Create a div in which the slider will be contained**
```css
  .card-categories {
    --gap: 1rem;
    padding-left: var(--gap);
  }
```
We defined a css variable named after "gap" to easily change the gap-spacing value if needed later
  We can reuse a variable using var(name-of-the-variable)

  **2. Define a div which is the slider**
```css
  .horizontal-slider {
    display: grid;
    grid-auto-flow: column;
    grid-auto-columns: minmax(180px, 1fr);
    grid-gap: var(--gap);
    overflow-x: auto;
    overscroll-behavior-x: contain;
    padding-bottom: var(--gap);
  }
```
`grid-auto-flow: column;` automatically makes n-elements live in n-columns. We conveniently don't need to specify the number of elements in our grid!
`grid-auto-columns: minmax(180px, 1fr);` each column will be 180px-wide minimum or 1-fraction-wide if larger than 180px.
`overflow-x: auto;` enables the horizontal scrolling
`overscroll-behavior-x: contain;` prevents the screen from bouncing at scrolling at the end of the slider

  **3. Show padding on the right-hand side when slider ends.**
```css
  .horizontal-slider:after {
    content: '';
    width: 1px;
  }
```
