## General

Use progressive enhancement and unobtrusive JavaScript. Core content and functionality should be delivered without requiring scripting. Browser support is well documented for many features at [caniuse.com](http://caniuse.com), use it.

In this spirit, _web components_ may be used experimentally using Polymer. Do not use for core content or functionality.

Build mobile first, using `min-width` media queries. Your code will better and more maintainable, and the download burden on clients will generally be more appropriate than with `max-width` media queries.

## HTML
HTML5 elements are well supported and may be used as standard. For IE8 and below, use IE conditional comments to load [html5shiv](https://github.com/afarkas/html5shiv), preventing extraneous http request when pollyfilling is not needed.

### Images
- Decorative images should be loaded as background images using CSS, controlled using media queries testing width and pixel density as required.
  
- Content images should be loaded from an `img` element with appropriate `alt` attribute. To serve responsive content images, use ```srcset``` and ```sizes``` attributes for equivalent images of different sizes and pixel densities. Use the ```<picture>``` element only for the art direction use case where the images are not equivalent. Polyfill all this with [Picturefill](https://github.com/scottjehl/picturefill). Note that this could cause a _lot_ of images to be used, so automate where possible. 

### Accessibility
- Sites should be [WCAG2](http://www.w3.org/TR/WCAG20/) AA compliant. Use WAI-ARIA features of HTML5 where appropriate, but don't overdo it. The W3C recently published useful [Notes on Using ARIA in HTML](http://www.w3.org/TR/aria-in-html/). Be mindful of how to implement aria live regions when sections within a page automatically update. 

### General notes
- Indentation should be exactly 2 spaces per level, no tabs. This applies to all human-authored font end files, e.g.: html, css, scss, js, svg etc.
- Every file should have exactly one blank line at the end.
- Don't use the `title` attribute. It doesn't help accessibility and implementations are all over the place. 

## CSS

If there's a standard for the existing codebase for quotes, (either double or single), stick to it.

For new codebases, or codebases without an existing standard, use only double quotes, not single quotes.

### Styleguide
- Indent with 2 spaces, one property per line, with a space between the selector and the opening brace. The colon separating the property name from its value should be followed by one space, but not be preceeded by a space.
 
 
```CSS
/* bad */
.block__element {
  color: currentColor; padding: 1em;
}

/* bad */
.block__element{
  color: currentColor;
  padding: 1em;
}

/* bad */
.block__element {
  color:currentColor;
  padding:1em;
}

/* good */
.block__element {
  color: currentColor;
  padding: 1em;
}
```
- When specifying multiple selectors for the same style rule, put each on a separate line:

```CSS
/* bad */
.block__element--modifier-1, .block__element--modifier-2 {
  padding: 1em;
}

/* good */
.block__element--modifier-1,
.block__element--modifier-2 {
  padding: 1em;
}

```

- List style rules alphabetically:
```CSS
/* bad */
.block__element--modifier {
  display: flex;
  color: rgb(0, 127, 255);
}

/* good */
.block__element--modifier {
  color: rgb(0, 127, 255);
  display: flex;
}
```

-  Leave one blank line between each style rule:

```CSS
/* bad */

.block__element_1 {
  display: inline-block;
}
.block__element_2 {
  display: inline-block;
}

/* good */

.block__element_1 {
  display: inline-block;
}

.block__element_2 {
  display: inline-block;
}
```


- Although using a double colon to describe pseudo elements is correct, we use a single colon. This is also (now) correct, and allows them to work correctly in IE 8.

```CSS
/* bad */
.block__element::after {
  content: '\0a00|\0a00';
}

/* good */
.block__element:after {
  content: '\0a00|\0a00';
}

```

- Use relative measures for font sizing (em, rem or %). When specifying font size, annotate with the calculation. This helps future you understand where the magic number came from:
 
```CSS
.block__element {
  font-size: 1.3125rem; /* 21px / 16px */
}
```

- Express `line-height` as a function of font size, rather than giving it units. 

```CSS
/* bad */
.block__element {
  font-size: 2em;
  line-height: 2.2em;
}

/* good */
.block__element {
  font-size: 2em;
  line-height: 1.1;
}
```

### General notes
- Concatonate and minify production code
- Use BEM for class nomenclature. See [Harry Robert's article](http://csswizardry.com/2013/01/mindbemding-getting-your-head-round-bem-syntax/).
- Keep selector specificity as low as possible, do not use ids for style-hooks.
- If you're thinking of using `!important`, think again. Then again. Still tempted? Please, once more... If you still really, truly believe you need to use it, then ask someone else before you do. If they agree it makes sense in your current use case, then go ahead (you should be feeling really dirty though), but document next to its use very clearly your rationale. If you do this well, future you might just let you off the hook. 
- Only chain selectors when really necessary. If you're using BEM properly, and also keeping specificity low, this should not be required very often.
- Prefer using selectors over creating extra markup just as style hooks. Useage examples of most selectors available at [http://davidcmoulton.github.io/css-selectors/](http://davidcmoulton.github.io/css-selectors/) [doesn't yet include shadow dom]. 
- When values depend on other values, try expressing those relationships in code (see line-height example in the Styleguide section).
- Prefer code that requires less maintenance. For example by expressing shadows as semitransparent black rather than a specific colour of grey, an element will be able to sit on a different background colour without requiring updating.

### SASS ###
- Where environment allows, use SASS to generate CSS stylesheets.
- Use `.scss` not `.sass` syntax.
- Use Compass.
- Avoid using `@extend`, use a `@mixin` instead (see http://www.sitepoint.com/avoid-sass-extend/).
- Generally speaking, structure using many partials compiling to one main CSS file. Keep the intent of each partial tightly focused. (This may be revised in the light of HTTP2, but stick with it for now.)
- Keep in mind the rules for CSS above when writing CSS with SCSS.
- Always generate sourcemaps. Check the sourcemaps actually work!

## Javascript
Use [ES5](http://es5.github.io/). This is standard in all mainstream browsers (but not IE8). Use common sense to play nicely using e.g. feature detection, and `try/catch` to prevent errors breaking all js in non-supporting clients. 

ES6 is coming but browser support is not there yet. At the moment our codebase is not complex enough to warrant authoring in ES6 and transpiling to ES5. This will be kept under review as support for ES6 improves and/or our codebase grows.

You can use the .jshintrc and .jscsrc files supplied in this repo to help enforce the rules that follow.

### Styleguide
Use [this code style guide](https://github.com/davidcmoulton/javascript/tree/master/es5). This is a slightly edited version of AirBnB's.

_Change from previous version:_ Now using *one `var` expression per variable*. Previously we were using one `var` statement per function, comma-separating individual variable declarations. This was fiddly when adding/removing variables due to potentially different line endings (`,` or `;`). Doesn't need to be backported, but when updating legacy code, please refactor to this style in one discreet commit to make merging back in easier.


### General notes
- Concatenate and minify production code (unless using HTTP2, in which case don't, and don't domain shard either)
- When determining what features to execute, use feature detection/duck typing rather than browser sniffing.
- Async load what code you can
- By default make sync code non-blocking by loading at the bottom of the body element. Exceptions are sometimes necessary, e.g. Modernizr, and html5shiv (aka html5shim) which must be loaded in the `<head>` element. If you need more control over async loading, you could use yepnope (comes with Modernizr, also available separately), or another async loading technique (Nicolas Zakas has some good ones).
- Favour event delegation over registering multiple event handlers on nested elements.
- Be aware that the capturing phase on an event is not supported in IE8 and can't be polyfilled.
- If you can, use CORS. Only use JSON-P if you trust the domain sending the data.


