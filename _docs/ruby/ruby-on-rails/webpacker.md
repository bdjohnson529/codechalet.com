---
title: "Webpacker"
layout: blog
order: 1
topic: Ruby
topic_path: /docs/ruby/index.html
---
Webpacker is a gem which wraps `webpack`, a Javascript tool for compiling and bundling assets (JS, CSS). When Webpack is executed within a project, it constructs a dependency graph of the Javascript code and generates an output set of Javascript files. These JS files are transferred to the client web browser.

In Rails 6, Webpacker is the default Javascript compiler, replacing sprockets (another library for compiling and bundling Javascript). 

# Packs
Webpack compiles assets (JS, CSS) into *packs*, which can be imported into a specific file in your application. Webpack has created an ERB helper method, [`javascript_pack_tag`](https://www.rubydoc.info/github/rails/webpacker/Webpacker%2FHelper:javascript_pack_tag), which creates an HTML script tag within a view.

Past versions of Rails used different package managers to compile assets, and saved assets in the `app/assets` directory. Rails 6 is integrated with webpack, and by convention assets are saved in `app/javascript/`. Admittedly, it is a little confusing to save CSS files and images in a folder named `javascript`, however, this is the default file structure and it is easy to work with if you accept the misnomer.

In the default configuration, Javascript packs are saved in `app/javascript/packs`. An `application.js` file can be used to import Javascript libraries which are necessary throughout the application. Javascript files specific to a page can be placed in separate files, within the `packs` folder. For example, the packs folder might look like this
```
├── app
|   ├── javascript
|       ├── packs
|           ├── application.js
|           ├── hello.js
```

To import `application.js` throughout the app, add the pack to `application.html.erb`:
```
<%= javascript_pack_tag 'application', 'data-turbolinks-track': 'reload' %>
```

# Webpack Entry Point
Webpack configuration is defined in `config/webpacker.yml`. This file defines the `packs` compiled by webpack. In the config file, the `source_entry_path` defines the folder automatically compiled by webpacker - the entry point webpacker will begin compiling your assets with the files in this folder.
```
source_path: app/javascript
source_entry_path: packs
```

# Plugins
The Webpack API has a [ProvidePlugin](https://webpack.js.org/plugins/provide-plugin/) function which automatically loads modules. To integrate a third-party Javascript library into your app, use `ProvidePlugin` within `config/webpack/environment.js`. For example, to include JQuery,

```javascript
const { environment } = require("@rails/webpacker");

const webpack = require("webpack");
environment.plugins.prepend(
  "Provide",
  new webpack.ProvidePlugin({
    $: "jquery/src/jquery",
    jQuery: "jquery/src/jquery",
  })
);

module.exports = environment;
```





## Further reading
* [Disable cache on Chrome](https://www.technipages.com/google-chrome-how-to-completely-disable-cache)
* [Rails Guides - Webpacker](https://edgeguides.rubyonrails.org/webpacker.html)
* [Understanding webpacker in Rails 6](https://prathamesh.tech/2019/08/26/understanding-webpacker-in-rails-6/)
* [Using webpacker in your RoR app deep dive](https://blog.appsignal.com/2021/02/17/using-webpacker-in-your-ruby-on-rails-app-deep-dive.html)
* [jQuery in Rails 6 Using Webpacker](https://www.botreetechnologies.com/blog/introducing-jquery-in-rails-6-using-webpacker/)