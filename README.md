# Page-block Framework
## REZO ZERO

- Maxime Bérard
- Ambroise Maupate

## Spec

- ES6 (convert with Babel)
- jQuery 2.2.0
- waitForImages
- debounce
- RequireJS

## Usage

- Install dependencies: `npm install` and `bower install`.
- Type `grunt` to convert ES6 scripts to `dist/` folder.
- Type `grunt build` to optimize project in one file in `build/` folder.

RequireJS bootstrap file :

```js
require.config({
    baseUrl: './dist',
    paths: {
        jquery: './../bower_components/jquery/dist/jquery.min',
        waitForImages: './../bower_components/waitForImages/dist/jquery.waitforimages.min',
        TweenLite: "./../bower_components/gsap/src/minified/TweenLite.min",
    }
});

require([
    'jquery',
    'router',
    'pages/page'
], function($, Router, Page) {
    var $body = $('body');
    var nodeType = $body[0].getAttribute('data-node-type') || 'page';
    var dataHome = $body[0].getAttribute('data-is-home');
    var bodyId = $body[0].id;
    var isHome = (dataHome == '1') ? true : false;

    var routerObj = new Router.default(
        {
            homeHasClass: false,
            ajaxEnabled: true,
        },
        {
            /*
             * Routes are nodeType corresponding to
             * ES6 modules
             */
            'page' : Page.default,
        },
        // temp namespace is defined in your index.html
        temp.baseUrl
    );
    routerObj.initEvents();
    routerObj.boot($('.page-content').eq(0), 'static', isHome);

    $('a').on('click', $.proxy(routerObj.onLinkClick, routerObj));
});
```