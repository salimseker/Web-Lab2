# Assignment 2 - Two Styles, One HTML Document

This project is a single HTML page (`index.html`) that can look like two completely
different layouts ("Version A" and "Version B") depending on which stylesheet it is
linked to. No JavaScript is used, only HTML and CSS, as required by the assignment.

## File Organization

- **`index.html`** - The only HTML file. It contains six `div` elements with the
  class `box` (the last one also has the class `last`, since it needs different
  styling in both versions). The document links to a single stylesheet through the
  `<link rel="stylesheet">` tag in the `<head>`. Swapping the `href` value between
  `styleA.css` and `styleB.css` is what changes the whole appearance of the page -
  the HTML itself never changes between the two versions.
- **`styleA.css`** - Produces "Version A": the six boxes stacked vertically and
  centered on the page, with a Flexbox column layout so the spacing between them
  grows or shrinks with the window while the boxes stay a fixed 100x100px.
- **`styleB.css`** - Produces "Version B": five boxes lined up horizontally in the
  top-left corner using `inline-block` + `white-space: nowrap` so they never wrap
  to a new line, plus a sixth box fixed to the bottom-right corner of the window
  with `position: fixed`.
- **`README.md`** - This file.

## Challenges Faced

- **Keeping the boxes centered but their spacing dynamic (Style A):** at first I
  tried using `margin` to separate the boxes, but that only adds space, it doesn't
  redistribute it when the window is resized. Switching the container to
  `display: flex; flex-direction: column;` with `justify-content: space-around`
  solved this, since Flexbox automatically re-distributes the empty space between
  items as the container size changes.
- **Making sure the boxes never resize:** by default, Flex items can shrink if
  there isn't enough room. I had to explicitly add `flex-shrink: 0` to the boxes so
  they keep their exact 100x100 (or 100x150) size no matter what happens to the
  window.
- **Borders changing the box size:** adding a `border` normally adds to the
  element's width/height instead of being included in it, which was making my
  boxes slightly bigger than 100px. Using `box-sizing: border-box` fixed this by
  making the border and padding count *inside* the declared width/height.
- **Preventing the boxes from wrapping (Style B):** by default, inline elements
  wrap to a new line if the window is too narrow. Combining `display: inline-block`
  on the boxes with `white-space: nowrap` on their parent keeps all five boxes on
  the same line, letting the page overflow horizontally instead of wrapping.
- **Pinning the last box to a corner of the window (Style B):** I needed the sixth
  box to always stay in the bottom-right corner, independent of the other boxes and
  independent of window resizing. `position: fixed` combined with `bottom`/`right`
  offsets took care of this, since it positions the element relative to the
  viewport instead of the normal document flow.
- **Two stylesheets, one HTML file:** the trickiest part conceptually was
  remembering that the HTML structure has to stay generic enough to support both
  layouts. Anything version-specific (colors, borders, positioning, hover effects)
  had to live entirely in the CSS files, not in the HTML.
