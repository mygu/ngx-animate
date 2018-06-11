# ngx-animate

[![npm](https://img.shields.io/npm/v/ngx-animate.svg)](https://www.npmjs.com/package/ngx-animate)

`ngx-animate` is a collection of cool, reusable and flexible animations for Angular. It implements all the animations in [animate.css](https://daneden.github.io/animate.css/), but with the power and flexibility of [Angular animations](https://angular.io/guide/animations) instead of CSS.

This library is thanks to [jiayihu<ng-animate>](https://github.com/jiayihu/ng-animate) for angular `4.2.0`.

This library will support more than version(`>=4.2.0 <7.0.0`).The creation of this library is because the original author is no longer updated, but my team needs higher angular version support.If you like, you can support it.(￣︶￣)

## Demo

The demo of the animations is available at [https://mygu.github.io/ngx-animate/](https://mygu.github.io/ngx-animate/).

## Usage

```
npm install ngx-animate --save
```

## Example

Import the animation from the package and pass it to your Angular component using [useAnimation](https://angular.io/api/animations/useAnimation):

```javascript
// my-component.component.ts
import { trigger, transition, useAnimation } from '@angular/animations';
import { bounce } from 'ngx-animate';

@Component({
  selector: 'my-component',
  templateUrl: 'my-component.component.html',
  animations: [
    trigger('bounce', [transition('* => *', useAnimation(bounce))])
  ],
})
export class MyComponent {
  bounce: any;
}
```

```html
<!-- my-component.component.html -->
<div [@bounce]="bounce"></div>
```

**Note**: Make sure to have included `BrowserAnimationsModule` in your `AppModule` and the [web-animation.js](https://github.com/web-animations/web-animations-js) polyfill.

It's also possible to import only a subset of the animations:

```javascript
import { bounce } from 'ngx-animate/lib/bouncing';
```

### Animation params

**All the animations** provided by `ngx-animate` support at least two **optional** params `timing` and `delay` to specify the animation duration and delay. Default value for `timing` is usually `1`s and `0`s for `delay`.  
You can pass the `params` object using the Javascript API or within the component template:

```javascript
@Component({
  selector: 'my-component',
  templateUrl: 'my-component.component.html',
  animations: [
    trigger('bounce', [transition('* => *', useAnimation(bounce, {
      // Set the duration to 5seconds and delay to 2seconds
      params: { timing: 5, delay: 2 }
    }))])
  ],
})
export class MyComponent {}
```

Using a template can achieve the same result, but you'll have access to the component context:

```html
<div [@bounce]="{ value: bounce, params: { timing: myTiming || 5, delay: myDelay || 2 } }"></div>
```

## Animations

All the animations are organized by their group. Many of them have additional params other than `timing/delay`: refer to [Advanced Usage](#advanced-params) for more details. Nevertheless you can probably ignore them if you're happy with how they are by default.

### Attention seekers

- `bounce`
- `flash`
- `pulse`
- `rubberBand`
- `shake`
- `swing`
- `tada`
- `wobble`
- `jello`

### Bouncing

- `bounceIn`
- `bouceOut`. Additional param: `scale`

The following bouncing animations have additional params `a, b, c, d` for `translate`

- `bounceInDown`
- `bounceInLeft`
- `bounceInRight`
- `bounceInUp`
- `bounceOutDown`
- `bounceOutLeft`
- `bounceOutRight`
- `bounceOutUp`

### Fading

All fading animations have additional params `fromOpacity, toOpacity` for `opacity` transition and `a, b` for `translate`.

- `fadeIn`
- `fadeInDown`
- `fadeInLeft`
- `fadeInRight`
- `fadeInUp`
- `fadeOut`
- `fadeOutDown`
- `fadeOutLeft`
- `fadeOutRight`
- `fadeOutUp`

### Sliding

Sliding animations are basically fading animations without a change of `opacity`. They can also receive the same params.

- `slideInDown`
- `slideInLeft`
- `slideInRight`
- `slideInUp`
- `slideOutDown`
- `slideOutLeft`
- `slideOutRight`
- `slideOutUp`

### Flippers

- `flip`
- `flipInX`
- `flipInY`
- `flipOutX`
- `flipOutY`

### LightSpeed

- `lightSpeedIn`
- `lightSpeedOut`

### Rotating

All rotating animations have additional params `fromOpacity, toOpacity` for `opacity` transition, `origin` for `transform-origin` and `degrees` for `rotate3d`.

- `rotateIn`
- `rotateInDownLeft`
- `rotateInDownRight`
- `rotateInUpLeft`
- `rotateInUpRight`
- `rotateOut`
- `rotateOutDownLeft`
- `rotateOutDownRight`
- `rotateOutUpLeft`
- `rotateOutUpRight`

### Specials

- `jackInTheBox`
- `hinge`
- `rollIn`
- `rollOut`

### Zooming

- `zoomIn`
- `zoomOut`

The following zooming animations have additional params `a, b` for `translate`

- `zoomInDown`
- `zoomInLeft`
- `zoomInRight`
- `zoomInUp`
- `zoomOutDown`
- `zoomOutLeft`
- `zoomOutRight`
- `zoomOutUp`

## Advanced params

Many of the animations support also other params like `scale`, `fromOpacity`, `toOpacity` and much more, allowing extremely flexible usage and customisation if you're not happy with default values. 

Single letters like `a, b, c, d` are used for the steps of some animations: `a` is the starting value, `d` is the ending.  
The animated property they refer to depends on the animation and the direction: usually `translate` on axis Y from `-Down/-Up`, axis X for `-Left/-Right`.

```javascript
useAnimation(bounceInDown, {
  params: {
    timing: 5,

    // Specify granular values for `translate` on axis Y during 'bounceInDown' 
    a: '-3000px',
    b: '25px',
    c: '-10px',
    d: '5px',
  }
})
```
