UI
====
- disables the Symfony UX Stimulus bridge
- Enabled Sass
- usage jquery

## Preparation
注意:  !!! at yarn V2 !!!
```
 如果没有 [yarn.lock](https://github.com/yarnpkg/berry/issues/2212) 文件, 在工程根目录新建一个空的.
```

- [install npm](https://tdtc-hrb.github.io/csdn/post/nodejs-ubuntu/)
- install yarn
```
sudo npm install --global yarn
```

### Sass
管理 JQuery && Bootstrap
```
yarn add sass --dev
yarn add sass-loader
```

- JQuery
```
yarn add jquery --dev
```

### update
- babel
- webpack

#### babel
```
yarn add @babel/core --dev
yarn add @babel/preset-env --dev
```
#### webpack
```
yarn add webpack --dev
yarn add webpack-cli --dev
yarn add webpack-notifier --dev
```
- webpack bridge
```
yarn add @symfony/webpack-encore --dev
```

### Bootstrap
```
yarn add @popperjs/core --dev
yarn add bootstrap --dev
```
#### v6 breaking changes
- Add new colors Sass partial, generate new CSS variables for tints and
[scss/_colors.scss](https://github.com/twbs/bootstrap/commit/7925387d5eda17500a837a068afb98c5cc3c7191#diff-6ec80b85fef778406fe6f5360b0c0e7fe08cecae0641ef8da62809af4f2392a9)
- [Remove jQuery support in plugins](https://github.com/twbs/bootstrap/commit/eda99074f887aaf3a43afd4cdb1fa28308962bdf)


## Asset Mapper
> 推荐在v8.4版本, 使用 AssetMapper
### [vendor - asset](https://symfony.com/blog/new-in-symfony-6-4-assetmapper-improvements#vendor-files-downloaded-locally)
- removed directory
```
assets/vendor
```
at .gitignore:
```
###> AssetMapper - Vendor Files Downloaded Locally ###
/assets/vendor/
###< AssetMapper - Vendor Files Downloaded Locally ###
```


## Sass
> webpack.config.js

- enables Sass/SCSS support
```
// enables Sass/SCSS support
.enableSassLoader()
```

### User config
- app.scss
add app.scss file of assets/styles
- app.js
import it at app.js:
```
import './styles/app.scss';
```

#### app.scss
Use
```
@use "~bootstrap/scss/bootstrap";
```
instead of
```
@import "~bootstrap/scss/bootstrap";
```

also see: [@import rules](https://sass-lang.com/documentation/breaking-changes/import/), 
[@use](https://sass-lang.com/documentation/at-rules/use/), 
and [Mixed declarations](https://github.com/twbs/bootstrap/issues/40621)


## [usage jquery](https://symfony.com/doc/current/frontend/encore/legacy-applications.html#accessing-jquery-from-outside-of-webpack-javascript-files)
- defer
- symbol

### defer off
config/packages/webpack_encore.yaml:
```xml
webpack_encore:
    # The path where Encore is building the assets - i.e. Encore.setOutputPath()
    output_path: '%kernel.project_dir%/public/build'
    # If multiple builds are defined (as shown below), you can disable the default build:
    # output_path: false

    # Set attributes that will be rendered on all script and link tags
    script_attributes:
        defer: false
```
### symbol
> $

asset/app.js:
```
// require jQuery normally
const $ = require('jquery');

// create global $ and jQuery variables
global.$ = global.jQuery = $;
```
