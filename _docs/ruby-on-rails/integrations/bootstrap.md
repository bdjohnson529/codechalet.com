---
title: "Bootstrap"
layout: blog
order: 3
topic: Rails
topic_path: /docs/ruby-on-rails/index.html
---
Note that rails 6 uses webpacker and so bootstrap integration is different from rails 5. This tutorial is transcripted from [Chris Lam's](https://www.youtube.com/watch?v=BIxd501hP-g) video on Youtube.

## Steps

Install bootstrap, jquery and popper.js
```bash
yarn add bootstrap jquery popper.js
```

Add the following to `config/webpack/environment.js`
```javascript
const webpack = require("webpack") 

environment.plugins.append("Provide", new webpack.ProvidePlugin({
  $: 'jquery',
  jQuery: 'jquery',
  Popper: ['popper.js', 'default']
}))
```

Add the following to `app/javascript/packs/application.js`
```javascript
import "bootstrap"
````

Add the following to `app/assets/stylesheets/application.scss`
```css
@import "bootstrap/scss/bootstrap"
```