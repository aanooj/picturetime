# PictureTime

A shot at a responsive images strategy that can be used today, it mimics the [proposed picture element](http://www.w3.org/community/respimg/wiki/Picture_Element_Proposal). Of course this is subject to change.

This takes much from Scott Jehl's [picturefill](https://github.com/scottjehl/picturefill) polyfill, but with the actual element.

**Note:** PictureTime includes (externally) the [matchMedia polyfill](https://github.com/paulirish/matchMedia.js/) which makes matchMedia work in `media-query`-supporting browsers that don't have `matchMedia`, or at least allows media types to be tested in most any browser. `matchMedia` and the `matchMedia` polyfill are not required for `picturefill` to work, but they are required to support the `media` attributes on `picture` `source` elements.

## Markup pattern and explanation

Mark up your responsive images like this. Redundancy in commented source is for IE9, as it won't read the innertext otherwise. Also, currently the fallback IMG is left in place for IE8.

```html
	<picture alt="Photo: Tiger in tall grass" />
		<!-- <source media="(min-width: 700px)" srcset="external/imgs/medium.jpg 1x, external/imgs/mediumplus.jpg 2x" /> -->
		<!-- <source media="(min-width: 900px)" srcset="external/imgs/large.jpg 1x, external/imgs/largeplus.jpg 2x" /> -->
		<!-- <source srcset="external/imgs/small.jpg 1x, external/imgs/smallplus.jpg 2x"> -->
	        <source media="(min-width: 900px)" srcset="external/imgs/large.jpg 1x, external/imgs/largeplus.jpg 2x" />
	        <source media="(min-width: 700px)" srcset="external/imgs/medium.jpg 1x, external/imgs/mediumplus.jpg 2x" />
	        <source srcset="external/imgs/small.jpg 1x, external/imgs/smallplus.jpg 2x"> 
	        
	        <!-- IE8 or non support fallback -->
	            <img data-src="external/imgs/medium.jpg" />
    </picture>
```

In order to prepare for the W3C's [resource priority specification](https://dvcs.w3.org/hg/webperf/raw-file/tip/specs/ResourcePriorities/Overview.html), PictureTime has been built with support for the `postpone` attribute, which delays loading of media until that media is visible on screen. To enable this feature, simply add `postpone` as an attribute to any picture element. Alternatively, you can use `postpone="[true|false]"` to explicitly turn this feature on or off respectively.

**Note:** If you are building a single-page app and your main content scrolls inside of a wrapper element rather than the window, then add `data-scroll-element="#myWrapper"` as an attribute to all the picture elements with the `postpone` attribute, where `#myWrapper` is some selector unique to the element in which the picture elements scroll.

