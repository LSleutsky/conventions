# `Web Performance`

A well-performing website is one which immediately engages users, keeps them on the page, and makes the UI a pleasure to interact with. But these things are hard to accomplish with a sluggish, latent product.

This repository contains the different performance optimizations that I've implemented to bring performance metrics in tools like Google's _[Lighthouse](https://developer.chrome.com/docs/lighthouse/overview/)_ and _[Page Speed Insights](https://pagespeed.web.dev/)_ from very low scores ranging between 10-20, to incredibly high scores upwards of 90-95.

## `What Is Web Performance?`

Simple - web performance is not only about making websites fast, but it's also about making slower processes _appear_ fast. Things like spinners, skeleton loaders, or other interactive UI elements that provide some sort of feedback to the user, while another process is preparing or loading, play a big part in the _perceived_ performance of a site, which can be just as important as the physical enhancements.

## `Where To Start?`

There are lots of different schools of thought on which facets of a web application should be prioritized to increase overall performance. The very concept of performance is usually approached with varied and subjective viewpoints. Things like accessibility, image optimizations, and things as basic as writing clean and organized code, all play a part in the raw speed of a website. To have a truly all-encompassing performant website, we also have to consider which device a user might be visiting the page on, and take into consideration the age of said device, as well as the connection speed.

Large, content-full website load drastically different on a desktop computer connected to a cable or fiber-optic network, versus a 5 year old tablet on a mobile network, versus that same tablet in an area or country with limited data coverage. The [Mozilla Developer Network's](https://developer.mozilla.org/en-US/) write-up [The "why" of web performance](https://developer.mozilla.org/en-US/docs/Learn/Performance/why_web_performance) states that a 22.6MB site like [CNN.com](https://www.cnn.com) could take 83 seconds to load on a 3G network, with the base HTML structure of the page clocking in at over 30 seconds.

## `Conversion Rates`

Decreasing the render time and download time of a website improves that site's conversion rate, which essentially relates to users on a site performing actions like clicking a link, making a purchase, or signing up for a newsletter. Performance increases conversion rates. The average user begins leaving a website when the loading time starts to pass 3 seconds, and most users are now on mobile devices, which natively take longer to load sites than do desktop sites, because of things like data connections based on the area where a user is located.

## `Low-Hanging Fruit`

Optimizing and making a web application fast is no easy feat. There are lots of moving parts to consider. Depending on the tech stack of the app, things like Babel optimizations, Webpack configurations, dead code, images, and code splitting, are just a few of the components that can - and should - be focused on. Assuming an ideal-world scenario, where bandwidth is unlimited and resource allocation is not a conern, when starting to optimize an existing app, the first area to focus on is auditing the code base at a high level, and removing the glaring areas of dead/unused code, and duplicate code. Going through the different files and checking for clean, modularized code that is DRY and actually in use, is a great first step.

## `Dependencies`

It's hard to find an app that doesn't use third-party npm libraries, and it's always great to be able to use the most updated versions of these dependencies. There is a way to declare which versions of the package you wish to use in your `package.json` file, by declaring a package in this manner:

```json
"react": "^16.9.0"
```

This will keep the version of React updated to the latest version 16, so that constantly incrementing to `16.10.0` or `16.11.0` is not necessary. This will cap the version at the first and main number of the package's version. At the time of this writing, React is on version 18, and using the latest version is not possible if we declare the dependency like above in our `package.json` file.

### `Changelog`

It's not as simple as just going into the `package.json` and arbitrarily updating a package to the latest version. There can be **_many_** breaking changes with a later version, and compatibility with your application could be very limited. It is critical that if considering to update a dependency to a later major version, to visit the package's home page and read thru a changelog, which lists all of the package updates, version by version, and includes breaking changes for specific versions.

The application being used for this documentation - which is a live application that I have contributed heavily to - is assumed to be on Webpack version `4.46.0`, which is the latest Webpack version 4, so we must exercise caution when updating third-party modules, taking care to scan the changelog to make sure the version we are choosing is compatible with the active Webpack version.

## `Webpack`

[Webpack](https://webpack.js.org/) is arguably the most popular application bundler out there. While many new and experimental - and marketed as faster - bundlers are now flooding the market, Webpack is a tried and true tool that has been part of countless projects. This particular repository assumes a Webpack-based application when taking into account the various performance considerations.

Webpack configurations consist of different `rules`, `optimizations`, and `plugins` that all play a part in creating an optimized, minified application that serves up a performant product to end users.

### `Rules`

Webpack `rules` configurations allow for different [loader](https://webpack.js.org/loaders/) configurations, which allow you to bundle static resources beyond JavaScript. One main performance point when it comes to Webpack `rules` is the [babel-loader](https://github.com/babel/babel-loader), which allows for transpiling JavaScript files with Webpack and Babel. The loader can be declared in a basic way to reap its benefits:

```js
const rules = [
  {
    test: /\.(js|jsx)$/,
    exclude: /node_modules/,
    include: path.join(__dirname, `app`),
    loader: `babel-loader`
  }

  ...
];

export default rules;
```

#### `Babel`

[Babel](https://babeljs.io/) is a JavaScript compiler that most modern frameworks leverage in order to be able to convert modern JavaScript syntax into a backwards-compatible version that can be run by older browsers. We will look at Babel optimizations more later on in this documentation.

The above allows for the `babel-loader` to be used with file extensions found in the `test` field, so long as those files are part of the `include`d directory. This _rule_ can be further optimized:

```js
const rules = [
  {
    test: /\.(js|jsx)$/,
    exclude: /node_modules/,
    include: path.join(__dirname, `app`),
    loader: `babel-loader`,
    options: {
      cacheDirectory: true,
      presets: [
        [
          `@babel/preset-env`,
          {
            modules: false,
            useBuiltIns: `usage`
          }
        ]
      ]
    }
  }

  ...
];

export default rules;
```

The `cacheDirectory` option aims to cache the results of the loader, and future Webpack builds attempt to read from the cache, to save expensive Babel recompilation processes. The `useBuiltIns` option is used so that Babel polyfills will be added automatically when the usage of some feature is unsupported in the target environment.

#### `Sass`

Sass is a popular CSS preprocessor used in most modern web applications that makes writing styles easier and more productive, allowing things like reusable utilities and CSS functions. To be able to use Sass in something like a React application, a loader needs to be setup in Webpack's `rules` configuration. We want to setup this rule to be optimized and utilize a more performance-centric pattern.

```js
const rules = [
  {
    loader: `sass-loader`,
    options: {
      sourceMap: true,
      webpackImporter: false,
      sassOptions: {
        outputStyle: `compressed`
      }
    }
  }

  ...
]

export default rules;
```

Another great performant Webpack loader is the `prerender-loader`, which does exactly what it's name implies. This loader also works closely with a common Webpack [plugin](#plugins) called the [HTML Webpack Plugin](https://github.com/jantimon/html-webpack-plugin).

```js
const rules = [ ... ];

if (!process.env.IS_DEVELOPMENT) {
  rules.push({
    test: path.join(__dirname, `index.html`),
    loader: `prerender-loader`,
    options: {
      string: true
    }
  });
}

export default rules;
```

### `Plugins`

In referring back to the [Low-Hanging Fruit](#low-hanging-fruit) section above, a great first Webpack plugin to leverage is called the [UnusedWebpackPlugin](https://github.com/MatthieuLemoine/unused-webpack-plugin). This plugin lives in your Webpack config's `plugin` array, and when the app is being built, looks for any and all unused files. The plugin can be set up in such a way that the build does not complete successfully if there are unused files found:

```js
import UnusedWebpackPlugin from 'unused-webpack-plugin';

...

const PATHS = {
  app: `path/to/app`,
  exclude: `path/to/exclude`
};

const plugins = [
  ...

  new UnusedWebpackPlugin({
    directories: [PATHS.app],
    exclude: [PATHS.exclude]
    failOnUnused: true
  })
];

export default plugins;
```

A directory in which to look for unused files - as well as what you wish to `exclude` - are useful parameters to provide this plugin to ensure there are no lingering unused files or assets weighing down your bundled site.

There are many other useful Webpack plugins that can greatly benefit performance gains:

```js
import BrotliPlugin from 'brotli-webpack-plugin';
import CompressionPlugin from 'compression-webpack-plugin';

...

const plugins = [
  ...

  new CompressionPlugin({
    filename: `[path][base].gz`,
    algorithm: `gzip`,
    test: /\.(js|(sc|c)ss|html|svg)$/,
    threshold: 10240,
    minRatio: 0.7
  }),
  new BrotliPlugin({
    filename: `[path][base].br`,
    test: /\.js$|\.(sc|c)ss$|\.html$|\.svg$/,
    threshold: 10240,
    minRatio: 0.7
  })
];

export default plugins;
```

The order of these above plugins is important. They control the compression components of the app during the bundling/minification process. Here, assets bigger than the `threshold` - and ones that compress better than the `minRatio` value - are processed. The `brotli-webpack-plugin` is not a typical-use-case Webpack compression plugin, and in order to gain the benefits from it, the application must be configured for Brotli compression in its final production state. If using [AWS](https://aws.amazon.com/) (_like this web application_), for example, it must be configured for [Brotli](https://en.wikipedia.org/wiki/Brotli) compression. On the client side, if using the common [Node.js](https://nodejs.org/en/) framework [Express](https://expressjs.com) and implementing compression paradigms, then the [express-static-gzip](https://github.com/tkoenig89/express-static-gzip) library is used, and it is possible to implement a preference for Brotli compression, with a Gzip fallback.

```js
const express = require('express');
const expressStaticGzip = require('express-static-gzip');

const app = express();

const PATHS = {
  app: `path/to/app`,
  bundle: `path/to/dist`
};

...

app.use(expressStaticGzip(PATHS.bundle, {
  enableBrotli: true,
  orderPreference: [`br`, `gz`],
  setHeaders: function (res, path) {
    res.setHeader("Cache-Control", "public, max-age=31536000");
  }
}));
```

Another very powerful plugin is the [Optimize CSS Assets Webpack Plugin](https://github.com/NMFR/optimize-css-assets-webpack-plugin), which optimizes and minimizes CSS assets:

```js
import OptimizeCssAssetsPlugin from 'optimize-css-assets-webpack-plugin';

const plugins = [
  ...

  new OptimizeCssAssetsPlugin({
    cssProcessorPluginOptions: {
      preset: [`default`, { discardComments: { removeAll: true } }]
    }
  })
];

export default plugins;
```

The above config also removes any comments found in your CSS styles, when bundling the app for production.

These plugins mentioned so far have been ones that can be used in both development and production environments alike. There are some Webpack plugins that are designed to exclusively work in production, and their benefits won't be felt or seen in a development environment, and can even sometimes worsen such an environment.

```js
import CrittersWebpackPlugin from 'critters-webpack-plugin';
import CssCleanupPlugin from 'css-cleanup-webpack-plugin';
import webpack from 'webpack';

const plugins = [ ... ];

if (!process.env.IS_DEVELOPMENT) {
  plugins.push(
    new CrittersWebpackPlugin({
      inlineFonts: true,
      keyframes: `critical`,
      noscriptFallback: true,
      preload: `swap`,
      preloadFonts: true
    }),
    new CssCleanupPlugin(),
    new webpack.AutomaticPrefetchPlugin()
  );
}

export default plugins;
```

The [CrittersWebpackPlugin](https://github.com/GoogleChromeLabs/critters) inline's the app's critical CSS and then lazy-loads the rest, on-demand. The [CssCleanupPlugin](https://github.com/do-web/css-cleanup-webpack-plugin) is plugin that aims to remove unused CSS and duplicate rules. Finally, the [AutomaticPrefetchPlugin](https://webpack.js.org/plugins/automatic-prefetch-plugin/) watches for modules from previous builds, and tries to improve on incremental build times.

### `Optimization`

The Webpack `optimization` array allows for a configuration which targets production-based performance optimizations.

The `minimize` parameter set to `true` is a very simple way to use Webpack's under-the-hood optimizations, which include [tree-shaking](https://webpack.js.org/guides/tree-shaking/) dead code removal. There is also a `minimizer` parameter, which allows you to set an optimization plugin that runs during compilation builds. Traditionally, the [TerserWebpackPlugin](https://github.com/webpack-contrib/terser-webpack-plugin) has been used in such optimizations, and now with the more modern addition of [ESBuild](https://esbuild.github.io/) in the tech world, we can use `TerserPlugin.esbuildMinify` to leverage the latter's optimizing goodness.

```js
import TerserPlugin from 'terser-webpack-plugin';

const optimization = {
  minimize: true,
  minimizer: [
    new TerserPlugin({
      cache: true,
      parallel: true,
      sourceMap: true,
      minify: TerserPlugin.esbuildMinify,
      terserOptions: {
        compress: {
          passes: 2
        },
        format: {
          comments: false
        },
        keep_fnames: true
      },
      extractComments: false
    })
  ],

  ...
};

export default optimization;
```

#### `Code Splitting and Chunks`

Code splitting consists of splitting code into various bundles which can then be lazy-loaded on-demand. As an app grows, so does the size of it, and code splitting is a paradigm which allows you to break down the size of large modules into smaller chunks, decreasing the weight of negative performance hits.

#### `Webpack Hints and Magic Comments`

Webpack has a pattern which is referred to as hints or magic comments. When implementing code splitting / lazy-loading, a common library that is used is the [Loadable Components](https://loadable-components.com/) library. This library is typically used over the native `React.lazy` and `React.Suspense` features because those native features do not work with server-side rendered apps, while the _Loadable Components_ library does.

When using _Loadable Components_ for code splitting imported components, the syntax looks like this:

```js
import loadable from '@loadable/component';

...

const loadableFallbackOptions = { ... };

const Component = loadable(
  () =>
    import (
      /* webpackChunkName: "Component" */
      /* webpackMode: "lazy" */
      /* webpackPrefetch: true */,
      `/path/to/component`
    ),
    loadableFallbackOptions
);
```

The `webpackChunkName` - as well as the other inline comments - are referred to as [Webpack magic comments](https://webpack.js.org/api/module-methods/#magic-comments). These awesome features let us name our chunks and select different loading modes. Some additional useful comments used for performance:

```js
/* webpackMode: "eager" */
/* webpackPreload: true */
```

The `lazy` mode generates a lazy-loadable chunk for each imported module, while the `eager` mode does not generate extra chunks, so no additional network requests are made. It is good and common practice to use `webpackPrefetch` with `lazy` mode, and `webpackPreload` with `eager` mode. The latter tells the browser that the resource _might_ be needed in the current navigation, and the former tells the browser that the resource is more than likely needed. These cool Webpack features are all related to the below optimization config:

```js
const optimization = {
  ...

  chunkIds: `total-size`,
  moduleIds: `size`,
  namedChunks: true,
  namedModules: true,
  runtimeChunk: `single`,
  splitChunks: {
    chunks: `all`,
    minSize: 30000,
    maxSize: 400000,
    minChunks: 1,
    maxAsyncRequests: 5,
    maxInitialRequests: 3,
    name: true,
    cacheGroups: {
      vendors: {
        name: `vendors`,
        test: /[\\/]node_modules[\\/](react|react-dom)[\\/]/,
        chunks: `all`,
        priority: -10
      },
      default: {
        minChunks: 2,
        priority: -20,
        reuseExistingChunk: true
      },
      styles: {
        name: `styles`,
        test: /\.(sc|c)ss$/,
        chunks: `all`,
        enforce: true
      }
    }
};

export default optimization;
```

### `Webpack Mode`

Another important and useful Webpack optimization is one of the most simple ones. In the main Webpack configuration file:

```js
const webpackConfig = {
  mode: `production`

  ...
};

export default webpackConfig;
```

Sets predefined Webpack production enhancements into place. If using one configuration file for both development and production builds, it's best to use a conditional to determine which environment we are currently in:

```js
const webpackConfig = {
  mode: process.env.IS_DEVELOPMENT ? `development` : `production`
  ...
};

export default webpackConfig;
```

## `Babel Optimizations`

There are also Babel optimizations that coincide with Webpack optimizations for a truly efficient application.

```js
comments: true,
env: {
  production: {
    plugins: [
      `@babel/plugin-transform-react-constant-elements`,
      [`babel-plugin-transform-react-class-to-function`, { memo: true }],
      [
        `transform-react-remove-prop-types`,
        {
          mode: `remove`,
          removeImport: true
        }
      ]
    ]
  }
},
plugins: [
  `lodash`,
  `transform-react-router-optimize`,
  `@babel/plugin-syntax-dynamic-import`,
  [
    `babel-plugin-styled-components`,
    { minify: true, pure: true, ssr: true, transpileTemplateLiterals: true }
  ],
  [
    `transform-imports`,
    {
      'react-bootstrap': {
        transform: importName => `react-bootstrap/lib/${importName}`,
        preventFullImport: true
      },
      lodash: {
        transform: importName => `lodash/${importName}`,
        preventFullImport: true
      },
      '@material-ui/core': {
        transform: importName => `@material-ui/core/${importName}`,
        preventFullImport: true
      }
    }
  ]
]
```

## `Dynamic Imports`

This is a very powerful `import` pattern which allows you to utilize imports as if they were promises, and import modules on demand. For example, if using something like [Firebase](https://firebase.google.com/), we can import dependencies dynamically, at the moment that we need them, instead of always importing heavy dependencies statically:

```js
async initialize() {
  const { initializeApp } = await import(`firebase/app`);

  ...
}
```

With `firebase/app`, we also need to import `firebase/auth` and `firebase/database`, both of which are very heavy libraries. So, we dynamically import them, so that we call on them as they are needed:

```js
async initialize() {
  const { initializeApp } = await import(`firebase/app`);

  await Promise.all([import(`firebase/auth`), import(`firebase/database`)]);

  ...
}
```

## `Image Optimizations`

Images are a critical component of most modern web applications, and when they are not properly optimized, they can have quite a negative impact on the performance of a website. There are numerous factors to consider, like:

- Size
- Format
- Quality

In performance audits, attributes like `width` and `height` are now considered crucial for proper image optimization, due to their effect on the [Cumulative Layout Shift](https://web.dev/cls/) of a site, which is a "glitch" of sorts, that causes a page to shift its contents by varying degrees, dependent on images that have not yet loaded, and end up rendering in the space which previously had an already rendered element. Adding the `width` and `height` attributes alleviates this jump in the screen.

```js
<img alt="Description" height="400" src="/path/to/image" width="600" />
```

### `imgix`

To save time in going thru hundreds of assets and either finding a UX resource to resize images, change their format, their quality, etc., an image service called [_imgix_](https://imgix.com/) was put into place. This image solution "_transforms, optimizes, and intelligently caches your entire image library for fast websites and apps using simple and robust URL parameters._"

What does this mean for our app? All of our assets are stored in an AWS S3 bucket. _imgix_ allows you to link and sync these buckets through their service, and then a URL is provided that routes the assets through _imgix's_ sources, allowing the addition of URL parameters to handle things like compression, image size, quality, dimensions, and much more.

In practice, it is very simple to leverage this service in an application. First, a util file is created for the _imgix_ service:

```js
const DEFAULT_PROPS = {
  auto: `compress,format`,
  fit: `crop`,
  cs: `tinysrgb`,
  q: `15`,
  fm: `avif`
};

const IMGIX_URL = `https://web.imgix.net/`;

const propsToParams = props => {
  const params = Object.entries(props).reduce((currentParams, prop) => {
    currentParams.push(`${prop[0]}=${prop[1]}`);

    return currentParams;
  }, []);

  return encodeURI(params.join(`&`));
};

export const getAwsAssetPath = (bucketUrl, props) => {
  const params = propsToParams({ ...DEFAULT_PROPS, ...props });

  return `${IMGIX_URL}${bucketUrl}?${params}`;
}
```

Then, when using images, we can simply get the asset source path by declaring:

```js
import * as Imgix from 'utils/imgix';

...

<img alt="Description" src={Imgix.getAwsAssetPath(`img/image.png`)} />
```

#### `Default imgix Config`

_imgix_ also allows you to set default parameters for images from within the account dashboard, so that they may serve as primary defaults, or as a fallback. There is an option to set a default image, which will render as a placeholder image if there is an issue with retrieving the desired image path. Conversely, you can also set a default error image, if the resulting image path will return an error:

![image-defaults](https://user-images.githubusercontent.com/7631797/172155701-c3475f2c-6762-4ac1-b379-24ee96b943ec.png)

As you can see from the above image, the `format` value is missing from the `auto` parameter in the default config for the _imgix_ source, but we are using `format` in our util. The reason is simple: the `auto` parameter accepts different values as defaults, but `format` is not one of them, so we have to include it manually. The _imgix_ service also allows setting caching policies for images:

![image-cache-settings](https://user-images.githubusercontent.com/7631797/172155698-d8342222-0a34-4d69-bf3d-97bb1f372ebf.png)

### `Lazy Loading`

For lazy-loading images, there are the terms above-the-fold and below-the-fold. For the latter, these are images that are not immediately visible when the site first loads, and the former are the immediate images that are in the viewport right when the site loads. Lazy-loading images involves putting emphasis on below-the-fold images, only loading them when they come into the viewport. To accomplish this, there is the [Intersection Observer API](https://developer.mozilla.org/en-US/docs/Web/API/Intersection_Observer_API), which is a utility that listens to a scroll event and observes changes in the intersection of a target element with an ancestor element or with a top-level element's viewport.

#### `lazysizes`

For a more automated and easier solution, the [_lazysizes_](https://github.com/aFarkas/lazysizes) library handles the lazy-loading of images for you, without the need for complex code. The implementation is incredible simple, after importing the `lazysizes` module somewhere in or near the highest level of your app, it's as simple as this:

```js
// index.js

import React from 'react';
import ReactDOM from 'react-dom';

...

import 'lazysizes';

ReactDOM.render( ... );
```

Then using the _lazysizes_ pattern on an `img` tag is very simple:

```js
// some-component.js

...

<img alt="Description" className="lazyload" data-src="/path/to/image" />
```

This can - and should - of course be combined with the _imgix_ service pattern:

```js
// some-component.js

import * as Imgix from 'utils/imgix';

...

<img alt="Description" className="lazyload" data-src={Imgix.getAwsAssetPath(`img/image.png`)} />
```

This will work the same way on an `Image` element imported from `next/image` in a Next.js application:

```js
// some-next-component.js

import Image from 'next/image';

import * as Imgix from 'utils/imgix';

...

<Image alt="Description" className="lazyload" data-src={Imgix.getAwsAssetPath(`img/image.png`)} />
```
