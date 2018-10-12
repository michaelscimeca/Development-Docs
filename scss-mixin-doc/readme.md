### Position
Easily set an element's position and "trbl" values.
Arguments: $type, $top, $right, $bottom, $left
The long way: @include position(relative, 5px, 5px, 10px, 15px)
Set absolute: @include absolute(10px, 25px, null, 50px)
Set relative: @include relative(10px, 35px)
Set fixed: @include fixed(null, null, 20px, 20px)
Note: Pass null as the value if you don't want a "trbl" property to be set.


```scss
@mixin position($type, $top: $position-default, $right: $position-default, $bottom: $position-default, $left: $position-default) {
  position: $type;
  $allowed_types: absolute relative fixed;
  @if not index($allowed_types, $type) {
    @warn 'Unknown position: #{$type}.';
  }
  @each $data in top $top, right $right, bottom $bottom, left $left {
    #{nth($data, 1)}: nth($data, 2);
  }
}
@mixin absolute($top: $position-default, $right: $position-default, $bottom: $position-default, $left: $position-default) {
  @include position(absolute, $top, $right, $bottom, $left);
}
@mixin relative($top: $position-default, $right: $position-default, $bottom: $position-default, $left: $position-default) {
  @include position(relative, $top, $right, $bottom, $left);
}
@mixin fixed($top: $position-default, $right: $position-default, $bottom: $position-default, $left: $position-default) {
  @include position(fixed, $top, $right, $bottom, $left);
}
```

***Example***

```scss
.element {
  @include position(absolute, null, null, 10px, 15px);
}
```

***Output***


```css
.element {
  position: absolute;
  bottom: 10px;
  left: 15px;
}
```

### Placeholder Color

```scss
@mixin input-placeholder {
  &.placeholder { @content; }
  &:-moz-placeholder { @content; }
  &::-moz-placeholder { @content; }
  &:-ms-input-placeholder { @content; }
  &::-webkit-input-placeholder { @content; }
}
```

***Example***

```scss
input,  
textarea {  
  @include placeholder {
    color: $grey;
  }
}
```

***Output***


```css
input::placeholder {
  color: #222222;
}
```

### Hide Text
Hide the text in an element.
```scss
@mixin hide-text {
  font: 0;
  color: transparent;
  text-shadow: none;
}
```

***Example***

```scss
.element {
  @include hide-text;
}
```

***Output***


```css
.element {
  font: 0;
  color: transparent;
  text-shadow: none;
}
```

### Em Calc
Calculate ems from a px value.

```scss
@function em($pxval, $base: $em-base) {

  @if not unitless($pxval) {
    $pxval: strip-units($pxval);
  }
  @if not unitless($base) {
    $base: strip-units($base);
  }

  @return ($pxval / $base) * 1em;
}
```



***Example***

```scss
.element {
  font-size: em(10px);
}
```

***Output***


```css
.element {
  font-size: 0.625em;
}
```

### Rem Calc
Calculate rems from a px value.
```scss
@mixin font-size($size, $base: 16) {
  font-size: $size; // fallback for old browsers
  font-size: ($size / $base) * 1rem;
}
```

***Example***

```scss
.element {
  @include font-size(16);
}
```

***Output***

```css
.body {
  font-size: 16px; // if no support for rem
  font-size: 1rem;
}
```

### Link Setup
Give your element all link events.

```scss
@mixin linksetup ($link, $visit, $hover, $active) {
  a {
    color: $link;
    &:visited {
      color: $visit;
    }
    @include hover {
      color: $hover;   
    }
    &:active {
      color: $active;
    }
  }
}
```

### Pseudo
When using ::before and ::after you'll always need these three, so we're saving two lines of code every time you use this.


```scss
@mixin pseudo($display: block, $pos: absolute, $content: '') {
  content: $content;
  display: $display;
  position: $pos;
}
```

***Exmaple***

```scss
div {
  &::after {
    @include pseudo;
  }
}
```

### Responsive Ratio
We use this for creating scalable elements (usually images / background images) that maintain a ratio.

***Untested***
```scss
@mixin responsive-ratio($x,$y, $pseudo: false) {
  $padding: unquote( ( $y / $x ) * 100 + '%' );
  @if $pseudo {
    &:before {
      @include pseudo($pos: relative);
      width: 100%;
      padding-top: $padding;
    }
    } @else {
      padding-top: $padding;
    }
  }
```
***Untested***
```scss
@mixin maintain-ratio($ratio: 1 1) {
  $width: 100%;
  $height: percentage(nth($ratio, 2) / nth($ratio, 1));

  width: $width;
  height: 0;
  padding-bottom: $height;
}
```

```scss
div {
  @include responsive-ratio(16,9);
}

div {
  @include maintain-ratio(16,9);
}
```

### Element Cover
```scss
@mixin cover() {
  position: absolute;
  top: 0;
  right: 0;
  left: 0;
  bottom: 0;
  width: 100%;
  height: 100%;
}
```

***Example***

```scss
.modal-background {
  @include overlay();
  background: black;
  opacity: 0.9;
}
```

### Desktop Hover
Desktop only. Requires you to attach `.no-touchevents` to HTML. Should be done by Medernizr.

```scss
@mixin hover {
  .no-touchevents & {
    &:hover {
      @content;
    }
  }
}
```

***Example***

```scss
@include hover {
  color: $hover;
}
```

  ### Viewport Units Calculator
  [Responsive CSS Mixin](http://emilolsson.com/tools/vw-unit-calc-an-online-responsive-css-font-size-calculator)

```scss
@function calc-vw($target) {
  $vw-context: (1440* 0.01) * 1px;
  @return ($target / $vw-context) * 1vw;
}

@function calc-vh($target) {
  $vh-context: (1440* 0.01) * 1px;
  @return ($target / $vh-context) * 1vh;
}
```


  ### Vertical Center The Unknown before Flex

```scss
@mixin vertical-center {
  &::before {
    content: '';
    display: inline-block;
    height: 100%;
    vertical-align: middle;
    margin-right: -0.25em;
  }

  > :first-child {
    width: 99.5%;
    display: inline-block;
    vertical-align: middle;
  }
}
```

***Example***

```scss
.container {
  @include vertical-center();
  .box {
    // Centered item
  }
}
```

### Media Queries Portrait & Landscape

```scss
/* ----------- iPhone 6 - 8 ----------- */
$phone-portrait: '(min-device-width: 375px)
                  and (max-device-width: 667px)
                  and (-webkit-min-device-pixel-ratio: 2)
                  and (orientation: portrait)';

$phone-landscape: '(min-device-width: 375px)
                   and (max-device-width: 667px)
                   and (-webkit-min-device-pixel-ratio: 2)
                   and (orientation: landscape)';

/* ----------- iPhone 6 - 8 Plus ----------- */
$phone-portrait-plus: '(min-device-width: 414px)
                       and (max-device-width: 736px)
                       and (orientation: portrait)
                       and (-webkit-min-device-pixel-ratio: 3)';

$phone-landscape-plus: '(min-device-width: 414px)
                        and (max-device-width: 736px)
                        and (orientation: landscape)
                        and (-webkit-min-device-pixel-ratio: 3)';

// /* ----------- iPhone X ----------- */
// $phone-portrait-x: '(min-device-width: 375px)
//                     and (max-device-width: 812px)
//                     and (-webkit-min-device-pixel-ratio: 3)
//                     and (orientation: portrait)';
//
// $phone-landscape-x: '(min-device-width: 375px)
//                      and (max-device-width: 812px)
//                      and (-webkit-min-device-pixel-ratio: 3)
//                      and (orientation: landscape)';

/* ----------- iPad ----------- */
$tablet-portrait: '(min-device-width: 768px)
                   and (max-device-width: 1024px)
                   and (orientation: portrait)
                   and (-webkit-min-device-pixel-ratio: 2)';

$tablet-landscape: '(min-device-width : 768px)
                    and (max-device-width : 1024px)
                    and (orientation : landscape)
                    and (-webkit-min-device-pixel-ratio: 2)';

/* ----------- iPad Pro ----------- */
$pro-tablet-portrait: '(min-device-width: 768px)
                       and (max-device-width: 1024px)
                       and (orientation: portrait)
                       and (-webkit-min-device-pixel-ratio: 2)';

$pro-tablet-landscape: '(min-device-width: 1112px)
                        and (max-device-width: 1112px)
                        and (orientation: landscape)
                        and (-webkit-min-device-pixel-ratio: 2)';


@mixin respond-to($media) {
  @media only screen and #{$media} {
    @content;
  }
}
```

***Example***

```scss
body {
  background-color: rgba(#1abc9c, .5);
  @include respond-to($phone-portrait) {
    background-color: rgba(#2ecc71, .5);
  }
  @include respond-to($tablet-portrait) {
    background-color: rgba(#3498db, .5);
  }
  @include respond-to($tablet-landscape) {
    background-color: rgba(#9b59b6, .5);
  }  
}
```
