# Adventures in AOM
Speaker: Rob Dodson  
Twitter: [@rob_dodson](https://twitter.com/rob_dodson?lang=en)

## What is AOM?
* Accessibility Object Model
* A proposed JS API to modify and explore web accessibility tree
  * fill in gaps in ARIA
  * Expose computed properties
  * Enable accessibility for custom-drawn UI
* [http://github.com/wicg/aom](http://github.com/wicg/aom)

## Filling in the gaps in ARIA
### Attribute and property parity
- role  
- ariaChecked  


```
setAttribute('role', ...);
```

```
<my-element aria-label="Hi">  
$('my-element').ariaLabel="Hi"
```
```
$('my-element').ariaControls=$(#some-id)
$('my-element').ariaLabelledby=[elementid…]
```

## A possible solution for labeling Shadow DOM? (read more)
- READ MORE
- GITHUB whatwg/html #3515
- ARIA 1.2 spec to read more

### Related:
https://medium.com/beginners-guide-to-mobile-web-development/accessibility-object-model-aom-part-1-8dc257fdb2d2

### CUSTOM ELEMENTS:
`<star-rating>`
### Original:
`<star-rating min="0" max"3" ...>`
### Rendered:
`<star-rating min="0" max"3 aria-valuemin="0" max="5" aria-valuemax="5" ...>`  

I want my components to have default semantics
```
classStarRating extends HTMLElement {
...
}

customElements.define("star-rating", StarRating, {
role: "slider",
ariaValueMin: min,
ariaValueMax: max,
ariaValueNow: val,
ariaValueText = `${val} stars`
});
```
```
<star-rating role="button" >
.. If role is removed, it will default to basic
<star-rating>
```
##  ARIA PRECEDENCE  
- ARIA is an explicit signal from the developer
- ARIA > per-instance > default

`
<star-rating aria-maxvalue="2">
`

[http://bit.ly/default-semantics](http://bit.ly/default-semantics)

## Does it work on a phone?
- Not at the moment!
- role="slider" asks to use volume buttons
- For events like increment, decrement, dismiss, scrollPageUp, scrollPageDown, ...
### Solution 1:
- Map actions to DOM events?

### Solution 2:
- Add new inputEvent types

### Proposed: 
- Virtual accessibility nodes  
[see photos in phone]

### How baked is this?
- ARIA 1.2 properties: - fairly baked
- Custom element semantics - waiting to be baked
- User action events - a tricky bake (can't label users using AT)
- Virtual accessibility nodes - baking!
- Computer accessible nodes - dessert (low priority)
- *TPAC will happen next week *

## AOM project link
[http://github.com/wicg/aom](http://github.com/wicg/aom)
