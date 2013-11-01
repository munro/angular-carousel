# AngularJS Touch Carousel

An AngularJS carousel implementation optimised for mobile devices.

Demo : http://revolunet.github.io/angular-carousel

Comments and contributions welcome :)

Proudly brought to you by the [@revolunet](http://twitter.com/revolunet) team.

## Usage :

 1. Add `angular-carousel.css`, `angular-carousel.js` and `angular-mobile.js` (from this repo) to your code:
```html
<link href="lib/angular-carousel.css" rel="stylesheet" type="text/css" />
<script src="lib/angular.js"></script>
<script src="lib/angular-mobile.js"></script>
<script src="lib/angular-carousel.js"></script>
```

 2. Add a dependency to the `angular-carousel` module in your application.
```js
angular.module('MyApp', ['angular-carousel']);
```

 3. Add a `rn-carousel` attribute to your `<ul>` block and your `<li>`'s become magically swipable ;)
```html
<ul rn-carousel class="image">
  <li ng-repeat="image in sportImages" style="background-image:url({{ image }});">
    <div class="layer">{{ image }}</div>
  </li>
</ul>
```
 4. You can also use `rn-carousel` without ng-repeat ;)
```html
<ul rn-carousel class="image">
  <li>slide #1</li>
  <li>slide #2</li>
  <li>slide #3</li>
</ul>
```
 5. Alternatively, for an infinite carousel, use the `rn-carousel-prev` and `rn-carousel-next` callbacks :
```html
<div rn-carousel-infinite rn-carousel-next="next(item)" rn-carousel-prev="prev(item)" rn-carousel-current="product">
  <h1> #{{ product.id }} </h1>
  {{ product.description }}
</div>
```

The `prev()` and `next()` function return promises containing the prev and next slide.

## Features :
 - Mobile friendly, tested on webkit+firefox
 - CSS 3D transformations with GPU accel

### Regular carousel :
 - `rn-carousel-index` two way binding to control the carousel position.
 - `rn-carousel-indicator` to turn on the indicator, see demo page.
 - `rn-carousel-buffered` to buffer the carousel, good to minimize the DOM.
 - ~~`rn-carousel-cycle` to have an forever-cycling carousel.~~ (BROKEN)
 - `rn-carousel-watch` force deep watch of the ngRepeat collection (listen to add/remove items).

## API :

You can access the carousel collection API by binding the carousel to a model.

```html
<ul rn-carousel ng-model="myCarousel">
    <!-- <li>...</li> -->
</ul>
<div class="rn-carousel-indicator">
    <span ng-repeat="item in myCarousel.items" ng-class="{active: $index==myCarousel.index}" ng-click="myCarousel.goTo($index)">●</span>
</div>
<a href="{{myCarousel.items[myCarousel.index].data_url}}">Learn More</a>
```

#### carouselModel.index

Get the current position of the carouselModel.

#### carouselModel.items

A list of all the carouselModel item's scopes.  You can also refernce the length with `carouselModel.items.length`.

#### carouselModel.goTo(index)

Jump to a slide in the carouselModel.  The index will wrap around.

#### carouselModel.next()

Go to the next slide.

#### carouselModel.prev()

Go to the previous slide.

### Infinite carousel :

 You can setup a dynamic, infinite carousel that will load slides on demand using a promise.
 - `rn-carousel-infinite` : use this to setup an infinite carousel without the initial ul/li structure.
 - `rn-carousel-next="getNextSlide(item)"` : callback called when carousel reach the last slide, that should return a single slide. great for generating slides on-demand.
 - `rn-carousel-prev="getPrevSlide(item)"` : callback called when carousel reach the first slide, that should return a single slide. great for generating slides on-demand.
 - `rn-carousel-current` : data-binding to the current carousel item. will be sent as first argument to the prev/next callbacks.

## Todo :
 - memory profiling
 - optional auto-slide
 - buffering : allow buffer size tuning (default=3 slides)
 - buffering : add intelligent indicators

## Inspirations
 - https://github.com/ajoslin/angular-mobile-nav
 - http://mobile.smashingmagazine.com/2012/06/21/play-with-hardware-accelerated-css/
 - Thanks @ganarajpr @bennadel and angular folks for all the tips :)

## Licence
As AngularJS itself, this module is released under the permissive [MIT license](http://revolunet.mit-license.org). Your contributions are always welcome.
