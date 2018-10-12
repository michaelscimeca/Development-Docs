# Browser Bugs

<img src="./findyou.jpg" width="450">


### List of Issues <a id="list-of-issues"></a>

## Outline<a name='outline'> </a>

1. [List Of Issues](#list-of-issues)
      - [FlexBox Issues](#flexbox-issues)
      - [IE Issues](#ie-issues)
      - [Chrome Issues](#chrome-issues)
      - [Css3 Transition Issues](#css3-transition-issues)

***
#### **FlexBox Issues** <a id="flexbox-issues"></a>
Flex Box list of issues at Github
[Flexbugs](https://github.com/philipwalton/flexbugs)

PostCSS [NPM](https://www.npmjs.com/package/postcss-flexbugs-fixes) tries to fix Flexbug's issues. `postcss-flexbugs-fixes` and with 1,473,981 download

***
#### **Audio on Mobile Issues** <a id="mobile-audio-issues"></a>
unlocking-web-audio-the-smarter-way
https://hackernoon.com/unlocking-web-audio-the-smarter-way-8858218c0e09
```js
function webAudioTouchUnlock (context) {
  return new Promise(function (resolve, reject) {
    if (context.state === 'suspended' && 'ontouchstart' in window) {
        var unlock = function() {
        context.resume().then(function() {
        document.body.removeEventListener('touchstart', unlock);
        document.body.removeEventListener('touchend', unlock);
        resolve(true);
      }, 
      function (reason) {
        reject(reason);
      });
    };
      document.body.addEventListener('touchstart', unlock, false);
      document.body.addEventListener('touchend', unlock, false);
    }
    else {
      resolve(false);
    }
  });
}
```

```js
webAudioTouchUnlock(context).then(function (unlocked) {
 if(unlocked) {
  // AudioContext was unlocked from an explicit user action,
  // sound should start playing now
  } else {
    // There was no need for unlocking, devices other than iOS
  }
},
function(reason) {
 console.error(reason);
});
```


***
#### **Chrome Issues** <a id="chrome-issues"></a>

##### **Scrollbar**
If you want to use a scrollbar-y you might need to use `::-webkit-scrollbar` with `-webkit-appearance: none;` to hide scrolls showing up on the chrome or safari.

```scss
&::-webkit-scrollbar {
  // display: none;
  -webkit-appearance: none;
}
```
***
#### **IE Issues** <a id="ie-issues"></a>

##### **Attribute**
When grabbing an attribute on DOM a element use `getAttribute` instead of `dataset`.

##### **Get Window XPosition in IE**
 `window.pageYOffset` instead of `window.scrollX`
[Issue Discussed](https://github.com/imgix/drift/issues/33)

##### **Get Dom XPostion in IE**
`Elm.getBoundingClientRect().x` Doesn't work in IE. Since IE doesn't provide x & y properties. Use `top` & `left`.




##### **Scrollbar** (Chrome & Safari tend to hide scrollbars)

```scss
-ms-overflow-style: -ms-autohiding-scrollbar;
-ms-overflow-style: none;
```
##### **X showing up on inputfields** (IE injects this into the DOM)

```scss
input {
  &::-ms-clear {
    display: none;
  }
}

```
##### **Down arrow on IE** (IE injects this into the DOM)

```scss
select {
  &::-ms-expand {
    display: none;
  }
}

```
***

**<sub>[Back to top](#outline)</sub>**


#### **CSS3 Transition Issues** <a id="css3-transition-issues"></a>

(Transitions issue)

🐛 **Known problem in (Safari, Firefox)**

If you find the transition element shifts or blurs.

- [Article on Chrome Flash Bug](https://www.sitepoint.com/fix-chrome-animation-flash-bug)
- [Article on Avoid CSS flickering](https://maximelafarie.com/avoid-css-flickering)

##### **Perspective**
When using transform properties you need to set a perspective. To activate 3D space, an element needs perspective. This can be applied in two ways: using the transform property, with the perspective as a functional notation.

[Some insight on Perspective](https://www.youtube.com/watch?v=8NGNKBIA_eI)
```scss
perspective: 1000;
perspective: 0;
```

##### **Transform Style**
By default, the descendants of an element are flattened into the plane of their parent. When you apply a 3D transform to an element, that element’s plane is no longer the default x-y plane—the plane of the display. All descendants of the element share that element’s new plane. To further transform the children of an element relative to that element’s plane, you must set the -webkit-transform-style property to preserve-3d, creating a 3D space. ([More on using 2d & 3d transforms](https://developer.apple.com/library/content/documentation/InternetWeb/Conceptual/SafariVisualEffectsProgGuide/Using2Dand3DTransforms/Using2Dand3DTransforms.html)) ([Stop CSS Animation Flicker](how-to-stop-css-animation-flicker-in-webkit))
```scss
transform-style: preserve-3d;
```
##### **Backface Visibility**
The ugly flicker during transitions which is caused by a CSS  called `backface-visibility`. Normally property is used, when you do 3D CSS transitions (e.g., 3D rotations). `backface-visibility` determines whether the backside of an HTML element is visible when it is not facing the screen. To fix the ugly flickering, you have to add the following to the CSS class:
[Backface Visibility](https://tympanus.net/codrops/css_reference/backface-visibility)
```scss
backface-visibility: hidden;
```

##### **Will-Change Properties**
Use this property sparingly. This lets browsers know about the kind of changes to be expected on an element so that the browser can set up appropriate optimizations ahead of time before the element is changed. Keep in mind that `will-change` is intended to be used as something of a last resort, to try to deal with existing performance problems. **NOTE:** No support in IE
```scss
will-change: transform;
```

##### **Possible Solutions**
```scss
#parent-elements {
  perspective: 700px;
  .child-element {
    transform-style: preserve-3d;
  }    
}
```

#### **Form Yellow Autocomple**
Full Article - [Ultimate list of hacks autocompleted inputs](http://webagility.com/posts/the-ultimate-list-of-hacks-for-chromes-forced-yellow-background-on-autocompleted-inputs)

```scss
.inputHoverFocus:-webkit-autofill:hover,
.inputHoverFocus:-webkit-autofill:focus {
    -webkit-box-shadow: 0 0 0 100px white inset;
    -webkit-text-fill-color: #f90;
}

```

#### **Loading Lifecycle**

(DOM loading issue)

🐛 **Known problem in (Safari / Slow Connection)**

- [DOMContentLoaded](https://kryogenix.org/days/2007/09/26/shortloaded)
- [Deep Dive On Page Lifecycle](https://javascript.info/onload-ondomcontentloaded)

Use this code below if you're going to grab location of DOM elements. Since Safari doesn't use the DOMContentLoaded the same way as Chrome, FireFox & IE. Using document.readyState, however, gives us property information about it.

```javascript
/**
There are three possible values:**
- "loading" – the document is loading.
- "interactive" – the document was fully read.
- "complete" – the document was fully read, and all resources (like images) are loaded too.
*/
document.onreadystatechange = function () {
  if (document.readyState === 'complete') {
    // Load Whatever
  }
};
```
**<sub>[Back to top](#outline)</sub>**
