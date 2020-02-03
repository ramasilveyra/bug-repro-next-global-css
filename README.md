# next.js bug with global CSS during SSR in development

Global CSS imported in `_app.js` is not injected on SSR during development.

> Note: production build links properly to global CSS build.

## Steps

1. Run `yarn dev`.
2. Go to http://localhost:3000.
3. Click on View Page Source, output doesn't has global css imported in `_app.js`. Eg:

```html
<!DOCTYPE html>
<html>
  <head>
    <style data-next-hide-fouc="true">body{display:none}</style>
    <noscript data-next-hide-fouc="true"><style>body{display:block}</style></noscript>
    <meta charSet="utf-8"/>
    <meta name="viewport" content="width=device-width,minimum-scale=1,initial-scale=1"/>
    <meta name="next-head-count" content="2"/>
    <link rel="preload" href="/_next/static/development/pages/index.js?ts=1580761922593" as="script"/>
    <link rel="preload" href="/_next/static/development/pages/_app.js?ts=1580761922593" as="script"/>
    <link rel="preload" href="/_next/static/runtime/webpack.js?ts=1580761922593" as="script"/>
    <link rel="preload" href="/_next/static/runtime/main.js?ts=1580761922593" as="script"/>
    <noscript id="__next_css__DO_NOT_USE__"></noscript>
  </head>
  <body>
    <div id="__next">
      <div>Hello!</div>
    </div>
    <script src="/_next/static/development/dll/dll_d6a88dbe3071bd165157.js?ts=1580761922593"></script>
    <script id="__NEXT_DATA__" type="application/json">{"props":{"pageProps":{}},"page":"/","query":{},"buildId":"development","nextExport":true,"autoExport":true}</script>
    <script nomodule="" src="/_next/static/runtime/polyfills.js?ts=1580761922593"></script>
    <script async="" data-next-page="/" src="/_next/static/development/pages/index.js?ts=1580761922593"></script>
    <script async="" data-next-page="/_app" src="/_next/static/development/pages/_app.js?ts=1580761922593"></script>
    <script src="/_next/static/runtime/webpack.js?ts=1580761922593" async=""></script>
    <script src="/_next/static/runtime/main.js?ts=1580761922593" async=""></script>
    <script src="/_next/static/development/_buildManifest.js?ts=1580761922593" async=""></script>
  </body>
</html>
```

4. But on CSR the css imported in `_app.js` is injected:

<img width="1792" alt="Screen Shot 2020-02-03 at 5 40 25 PM" src="https://user-images.githubusercontent.com/7464663/73689173-6883aa80-46ac-11ea-876f-e47d8fe9bef0.png">

