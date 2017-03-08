# crds-styles

`crds-styles` provides the primary CSS framework and global style patterns that power [crossroads.net](http://crossroads.net) and it's related properties. Any elements and/or implementation details included within the [Digital Design Kit (DDK)](http://github.com/crdschurch/crds-styleguide) are provided by this NPM package. Any deviations from the patterns defined there should be implemented in the client application.

## Implementation

Until this project is published to NPM, you have two options to get it included as a dependency of your Node compatible application.

---

### Option #1 - Symlink Local Directory

Assuming the `crds-styles` repo resides in the same local directory as your project, you can do the following to setup the symlink...

    $ cd path/to/your/project-directory
    $ npm link ../crds-styles

### Option #2 - Reference Github URL in package.json

If you don't have the DDK cloned locally, you can just reference the repo directly in your `package.json` file, like so...

    {
      "name": "foo",
      "version": "0.0.0",
      "dependencies": {
        "crds-styles": "crdschurch/crds-styles"
      }
    }

---

Once you've added `crds-styles` to `package.json` you need to import the stylesheet in your application's main '.scss' file using the following convention. You can optionally override any of the customizable Bootstrap variables prior to import...

    @import '~crds-styles/assets/stylesheets/bootstrap';

## SVGs

Any project consuming `crds-styles` will need to update their build process in order to access SVG files. For information on adding new icons to `crds-styles` please refer to [the documentation](https://github.com/crdschurch/crds-styles/blob/development/assets/svgs/README.md).

### Webpack build
If using webpack, the `copy-webpack-plugin` can be used to move the svg files to the distribution folder
```javascript
plugins: [
    new CopyWebpackPlugin([
      {
        context: './node_modules/crds-styles/assets/stylesheets/svg/assets',
        from: '*.svg',
        to: 'assets',
      }
    ])
  ]
```
See `crds-styleguide` [`webpack.common.js`](https://github.com/crdschurch/crds-styleguide/blob/development/config/webpack.common.js) for a full example

### Webpack Dev Server
If using `webpack-dev-server` as a development tool, the implementation will need to be modifed to support `content-base` which will serve static assets from the given directory as well as trigger a build in order to have `CopyWebpackPlugin` triggered to move SVGs
```json
"scripts": {
    "serve": "npm run start",
    "start": "npm run build-dev && webpack-dev-server --inline --open --progress --port 4200 --content-base dist/",
    "build-dev": "rimraf dist && webpack --config config/webpack.dev.js --progress --profile --bail",
}
```
See `crds-styleguide` [`package.json`](https://github.com/crdschurch/crds-styleguide/blob/development/package.json) for a full example.

## Versions &amp; Roadmap

We'll be developing the pattern library over the next few months and as we release new updates, we will increase the version number according to the following rules.

* Bug fixes and other minor changes: Patch release, increment the last number, e.g. 1.0.1
* New features which don't break existing features: Minor release, increment the middle number, e.g. 1.1.0
* Changes which break backwards compatibility: Major release, increment the first number, e.g. 2.0.0

Once we reach version 1.0.0, the DDK will be feature complete and will continue to be updated in manner described above.

## License

This project is licensed under the [3-Clause BSD License](https://opensource.org/licenses/BSD-3-Clause).
