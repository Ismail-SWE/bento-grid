# Frontend Mentor - Bento Grid Solution

This is my solution to the [Bento grid challenge on Frontend Mentor](https://www.frontendmentor.io/challenges/bento-grid-RMydElrlOj).

## Table of contents

- [Overview](#overview)
  - [The challenge](#the-challenge)
  - [Screenshot](#screenshot)
  - [Links](#links)
- [My process](#my-process)
  - [Built with](#built-with)
  - [What I learned](#what-i-learned)
  - [Continued development](#continued-development)
  - [AI Collaboration](#ai-collaboration)
- [Author](#author)

## Overview

### The challenge

Users should be able to:

- View the optimal layout for the interface depending on their device's screen size

### Screenshot

![](./screenshot.png)

### Links

- Solution URL: [GitHub](https://github.com/Ismail-SWE/bento-grid)
- Live Site URL: [Live Site](https://ismail-swe.github.io/bento-grid/)

## My process

### Built with

- Semantic HTML5 markup
- CSS Grid
- Flexbox
- CSS custom properties
- Mobile-first responsive design

### What I learned

**1. grid-template-areas — naming grid zones**

Starting with named areas felt the most readable way to visualize the layout:

```css
.grid {
    grid-template-areas:
        "create  hero    hero     schedule"
        "create  manage  consist  schedule"
        "ai      audience  grow   grow";
}

.card-create   { grid-area: create; }
.card-hero     { grid-area: hero; }
```

**2. Line-based placement — grid-column and grid-row**

I later switched to line-based placement for more precise control over how many rows each card spans:

```css
.card-create   { grid-column: 1;          grid-row: 1 / span 3; }
.card-hero     { grid-column: 2 / span 2; grid-row: 1 / span 2; }
.card-schedule { grid-column: 4;          grid-row: 1 / span 4; }
```

**3. overflow: hidden — intentional image bleeding**

Cards use `overflow: hidden` to clip images that bleed past the card edges. Negative margins push images outside the padding boundary:

```css
.card {
    overflow: hidden;
    padding: 1.5rem;
}

.card-consistent__img {
    margin-bottom: -1.5rem; /* bleeds past bottom edge */
    width: calc(100% + 3rem); /* stretches past side edges */
    margin-left: -1.5rem;
}
```

**4. position: absolute needs position: relative parent**

When positioning an image absolutely inside a card, the card itself needs `position: relative` — otherwise the image escapes to the nearest positioned ancestor:

```css
.card-schedule {
    position: relative; /* without this, image escapes the card */
}

.card-schedule img {
    position: absolute;
    bottom: 0;
}
```

**5. CSS custom properties — reusable values**

```css
:root {
    --purple-500: hsl(256, 67%, 59%);
    --yellow-500: hsl(39, 100%, 71%);
    --purple-100: hsl(254, 88%, 90%);
    --yellow-100: hsl(31, 66%, 93%);
}
```

**6. Figma style guide — design tokens to CSS**

Working from a Figma style guide made typography much more precise. Instead of eyeballing values, I matched exact specs:

```css
.card-hero__title {
    font-size: 2.5rem;
    line-height: 0.935;
    letter-spacing: -2px; /* directly from Figma */
}
```

**7. grid-template-rows — controlling row heights**

Without explicit row heights, rows expand to fit their content unevenly. Adding `repeat(6, 1fr)` made all rows equal height:

```css
.grid {
    grid-template-rows: repeat(6, 1fr);
    height: 850px;
}
```

**8. Sketching grid layout before coding**

Before writing any CSS, mapping out the grid visually — which card spans how many columns and rows — saved a lot of trial and error. The bento layout has 4 columns and 6 rows with cards spanning different areas.

**9. flex-direction: row — horizontal card layout**

The "Grow followers" card places the image and text side by side:

```css
.card-grow {
    display: flex;
    flex-direction: row;
    align-items: center;
    gap: 1.5rem;
}

.card-grow__img {
    width: 50%;
    flex-shrink: 0;
}
```

**10. margin-top: auto — pushing content to the bottom**

Inside a flex column, `margin-top: auto` on an image pushes it to the bottom of the card while keeping the title at the top:

```css
.card-create {
    display: flex;
    flex-direction: column;
}

.card-create img {
    margin-top: auto;
}
```

### Continued development

- Building fully responsive layouts without relying on fixed pixel heights
- Getting more comfortable reading and implementing designs directly from Figma
- Writing cleaner, more organized CSS — especially avoiding conflicts between general rules like `.card img` and specific overrides
- Adding smooth CSS transitions and hover effects

### AI Collaboration

- **Tool:** Claude (Anthropic)
- **How:** Used for learning CSS Grid concepts, debugging layout issues, analyzing Figma designs, and understanding how grid placement strategies differ
- **What worked well:** Going step by step — reset, body, grid container, grid areas, then each card one by one — made the process much clearer than trying to write everything at once. Getting instant feedback on screenshots helped catch issues early
- **What didn't:** Some sizing values still needed manual trial and error — AI cannot always predict the exact visual result without seeing the rendered output

## Author

- Frontend Mentor - [@Ismail-SWE](https://www.frontendmentor.io/profile/Ismail-SWE)
- GitHub - [@Ismail-SWE](https://github.com/Ismail-SWE)