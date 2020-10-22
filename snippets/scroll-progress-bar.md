---
title: Scroll Progress Bar
tags: interactivity,intermediate
---

Creates a progress bar that will show the progress on scrolling with color indication.

- It calculates the scroll percentage on `scroll` event and feed it to the progress bar to grow.
- Based on the scroll percentage it will generate the RGB value (Used string interpolation to make RGB values dynamic).
- `--color` and `--bar-width` are custom properties defined to modify the value on scroll.

```html
<div class="progress-bar"></div>
```

```css
body, html {
  height: 500px;
}
.progress-bar {
  position: fixed;
  top:40%;
  left:20%;

  height: 16px;
  width: 900px;

  border-radius: 8px;
  box-shadow: 0 0 1px 1px rgba(0, 0, 0, 0.15), inset 0 8px rgba(255, 255, 255, 0.2);
  background: linear-gradient(to right, var(--color) var(--bar-width), transparent 0);
}
```

```js
document.addEventListener(
  "scroll",
  function() {
    let scrollTop = document.documentElement["scrollTop"] || document.body["scrollTop"];
    let scrollHeight = (document.documentElement["scrollHeight"] || document.body["scrollHeight"]) - document.documentElement.clientHeight;
    
    let scrollPercent = scrollTop / scrollHeight * 100 ;
    let color =  `rgb(${Math.abs(244 - (scrollPercent * 1.5))}, ${(scrollPercent * 1.5) + 64}, 31)`;
    
    let progressBar = document.querySelector(".progress-bar");
    progressBar.style.setProperty("--color", color);
    progressBar.style.setProperty("--bar-width", (scrollPercent + "%"));
  },
  { passive: true }
);
```
