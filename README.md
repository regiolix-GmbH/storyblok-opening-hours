# Storyblok Opening Hours

> A Storyblok field-type for managing opening hours.

## How to use

Storyblok Opening Hours is a custom field type plugin for the headless CMS Storyblok. In order to use it, you have to build and install it first.

### Deployment

You can start by cloning this repository and installing its dependencies.

```bash
git clone git@github.com:maoberlehner/storyblok-opening-hours.git
cd storyblok-opening-hours
npm install
```

Because Storyblok plugins share a global namespace, you have to choose a distinct name for your plugin first. Go to `src/Plugin.vue` and change the following line of code.

```diff
         ],
         // This is the name of our plugin.
-        plugin: `opening-hours`,
+        plugin: `YOUR-DISTINCT-NAME`,
       };
     },
```

Now you can run the build command and copy and paste the generated code into Storyblok when it's done.

```bash
npm run build
```

Next go to the [Plugins page](https://app.storyblok.com/#!/me/plugins) and click the `New` button in the top right. It is important to choose the same name you specified in the `initWith()` method for your plugin to work. After creating a new plugin you can copy the contents of `dist/export.js` into the plugin editor.

## Build Setup

```bash
# Install dependencies.
npm install

# Serve with hot reload at localhost:8080.
npm run dev

# Build for production.
npm run build
```

## About

### Author

Markus Oberlehner  
Website: https://markus.oberlehner.net  
Twitter: https://twitter.com/MaOberlehner  
PayPal.me: https://paypal.me/maoberlehner  
Patreon: https://www.patreon.com/maoberlehner

### License

MIT
