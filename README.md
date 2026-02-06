https://www.su-and-gem.com


## Adding a new year's valentine

1. **Add images** to `we love you_files/`: `YYYY_front.jpg` and `YYYY_back.jpg` (or `.gif` if needed).
2. **Preload the back image**: In `index.html`, add `'we love you_files/YYYY_back.jpg'` (or `.gif`) to the `MM_preloadImages(...)` list in the `<body onload="...">` attribute.
3. **Add the valentine block**: Insert a new `<p>` at the top of the valentine list (right after the email `<pre>`). Use a unique `id` (e.g. `Image25` for the next year) and this pattern:

```html
<p align="center"><img src="./we love you_files/YYYY_front.jpg" id="ImageNN" onmouseover="MM_swapImage('ImageNN','','we love you_files/YYYY_back.jpg',1)" onmouseout="MM_swapImgRestore()">
```

Replace `YYYY` with the year and `ImageNN` with a unique id not used elsewhere on the page.

**Unique id required:** Each valentine image must have a different `id`. If two images share an id, `getElementById()` returns only the first one, so the hover swap will target the wrong card (or the second card will never swap). Use the next unused id in sequence (e.g. after `Image24` and `Image25`, use `Image26`).


## How the page is built and rendered

**Build:** None. The site is static. There is no build step, bundler, or generator. You edit `index.html` and add/replace files in `we love you_files/`; the repo is the source of truth and is deployed as-is (e.g. static host or GitHub Pages; `CNAME` is for the custom domain).

**Data:** All content lives in the repo. Valentine “data” is (1) the HTML: each year is one `<p>` with an `<img>` and `onmouseover`/`onmouseout` handlers, and (2) the assets: `we love you_files/YYYY_front.*` and `YYYY_back.*` (jpg or gif). There is no CMS, database, or separate data file. Order of valentines is the order of those `<p>` elements in `index.html` (newest first).

**Rendering:** The browser loads `index.html`. On `body` load, `MM_preloadImages(...)` preloads each year’s back image so hover is instant. Each valentine image has inline handlers that call `MM_swapImage(id, '', backImagePath, 1)` on mouseover and `MM_swapImgRestore()` on mouseout (Dreamweaver-style image swap). The script block in `<head>` defines those functions; no external JS.
