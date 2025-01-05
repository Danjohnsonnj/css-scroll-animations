# css-scroll-animations

Recreate JS based scroll animations using the new CSS APIs, plus some additional leading edge CSS features.

Viewable on modern Chromium browsers at [here](https://danjohnsonnj.github.io/css-scroll-animations/index.html).

# Demo

The current version of the experiment is viewable via Github Pages: [danjohnsonnj.github.io/css-scroll-animations/](https://danjohnsonnj.github.io/css-scroll-animations/).

# A description of some CSS features used

## Native CSS Nesting

- A code organization feature common to CSS preprocessors like LESS is now available to many browsers natively. Nesting helps developers by reducing the need to repeat selectors while also co-locating style rules for related elements. It can also help styles match the HTML they target.

## Feature support queries

- This type of query can be used to conditionally apply CSS rule sets based on whether or not the browser supports particular features, properties and/or values. It can take a chained set of queries with `and`, and can also test the negative with `not`.

## Keyframe animations

- The `@keyframes` CSS at-rule controls the intermediate steps in a CSS animation sequence by defining styles for keyframes along the animation sequence. Keyframe timelines can also update non-animatable properties, which can come in handy, for example by using custom properties and style queries to apply different rule sets throughout the sequence.

## Breakdown by page section

### Pure CSS banner

- Throughout this demo I rely CSS custom properties for many uses. In this case they are used as part of the infinitely running "blink" keyframe animation on the "pure css" text, giving a sort of neon sign behavior.
- Position sticky is used to control the positioning of the "This is" text, allowing it to meet the "pure css" text before moving with the scroll.
- A named view timeline is set on the wrapper container. The "pure css" text references that ancestor timeline to as its animaiton timeline for a keyframe animation controlling its position, scale, opacity and visibilty.

### Reading Progress Bar

- Position sticky is used to keep the progress bar in view over the relevant "article" text.
- The bar is animated using a named view timeline on the article body, filling the progress bar by starting when the article comes into the viewport, and completing when it leaves.

### Fixed Section

- Again, a named view timeline used as the animation timeline for the text. In this case the text moves quickly through a portion of the scroll, then matching the scroll amount and text translation amount to make it appear to be fixed. This can't quite be achived either with sticky or fixed positioning.

### Profile Cards

- This section contains profile card that each have their own view timeline, so the keyframe animation applied to it is based on its own position within the viewport. The cards "fall" into view as the come into the viewport.
- As you hover over each card, the others become deemphasized, and its background animates. This is done with a combination of the `:hover` and `:not` pseudo selectors, as well as the new `:has` pseudo selector, which has sometimes been describe as an ancestor selector.
- The animation of the background is through a transitioned clip path, hiding and revealing portions of the element.

### Scroll Snap Carousel Gallery

- The gallery uses scroll snapping to ensure that each child image will be positioned within the center of the container. As you scroll a bit to the left or right and release, it will snap back to the center. Once you move beyond a thresold of distance, the container will snap to the next most appropriate image.
- The "active" state is achieved through the use of a named view timeline on the horizontally scrolling carousel, adjusting the saturation and opacity of the images.

### Parallax sections

- These are done using the methods described above: a named view timeline used as the animation timelines, offsetting the elements in relationship to how much of the section is in view. In the staggered example, multiple timelines are used with the same keyframe animation, but the offsets for the appearnace of distance is achieve by changing the range used to watch the section in the viewport, extending beyond its bounds to slow down their movement.

### Trigger section

- This section is an example of animating non-animatible CSS properties: in this case a custom property, changing it like a boolean from false to true and back. It then uses a style query on the element being animated to check if the custom property is true, triggering the applicaiton of an additional ruleset to make a child element position fixed. As you continue to scroll, the boolean goes back to false and the ruleset is no longer applied.

### Filigree section

- This is a failed experiment! The "drawing" effect is achieved through the use of SVG stroke dash array and stroke dash offset. These properties control the spacing between "dashes" of the line used as a stroke for an SVG path. By setting the spacing of the dash to the same length as the path and offsetting it by that amount, the entire path will be contained by that gap between dashes, appearing to have no stroke. By animating the offset, an author can make it appear that the SVG is being drawn as the dash moves to replace the empty gaps. I was not able to control the adjustment of the dash offset using a named view timeline and animation timeline, instead triggering the animation as above and using a transition.

## Other features

A description of other features used on this page are in the footer of the site.
