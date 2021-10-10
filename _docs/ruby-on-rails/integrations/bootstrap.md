---
title: "Bootstrap"
layout: blog
order: 3
topic: Rails
topic_path: /docs/ruby-on-rails/index.html
---
Note that rails 6 uses webpacker and so bootstrap integration is different from Rails 5. Bootstrap relies on a the popper.js library, so this tutorial shows how to install both. This tutorial assumes that you have configured Webpacker to compile both javascript and stylesheet assets. For instructions on doing this, please see the [Webpacker tutorial](/docs/ruby-on-rails/integrations/webpacker.html).

## Install node modules
Install bootstrap.
```bash
yarn add @popperjs/core bootstrap
```

Your `package.json` should now include both packages. Your versions will likely be different than the ones displayed below.
```json
"dependencies": {
  ...
  "@popperjs/core": "^2.10.2",
  "bootstrap": "^5.1.3",
}
```

## Configure webpacker
Add the following to `app/frontend/packs/application.js`.
```javascript
import "bootstrap"
```

Add the following to `app/frontend/stylesheets/application.scss`.
```css
@import '~bootstrap/scss/bootstrap';
```

Add the following to `config/webpack/environment.js`.
```javascript
// config/webpack/environment.js

const { environment } = require('@rails/webpacker');
const webpack = require("webpack");

environment.plugins.append("Provide", new webpack.ProvidePlugin({
    Popper: ['popper.js', 'default']
  })
);

module.exports = environment
```
