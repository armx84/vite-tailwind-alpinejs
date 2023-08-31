# vite-tailwind-alpinejs
This repo shows the configuration to use Vite Vanilla with AlpineJS and TailwindCSS

## Why this repo
Vite is mostly used with Vue and similar frameworks. Here we are using it with AlpineJS and TailwindCSS.

## Try it out

To test this package just run:
```cli
npm install
```

and then do
```cli
npm run dev
```
Navigate to the URL provided to see AlpineJS and TailwindCSS loaded.
Thre's also a third party Javascript (huge) library like Monaco Editor added.

All bundled by Vite.


*Packages installed*:
```json
"devDependencies": {
    "tailwindcss": "^3.3.3",
    "vite": "^4.4.5",
    "postcss": "^8.4.28",
    "autoprefixer": "^10.4.15"
  },
  "dependencies": {
    "alpinejs": "^3.13.0",
    "monaco-editor": "^0.41.0"
  }
```

## Vite
The Vite project has been created with a Vanilla template. This template has then been modified to use TailwindCSS and Alpine.

We are NOT mounting any app per se. We are only initializing AlpineJS.
Vite looks for

Vite has been configured with a custom configuration file in:
```cli
vite.config.js
```
to use the *src* folder for source files instead of the root folder.

```json
export default {
    root: 'src',
    build: {
      outDir: '../dist'
    }
  }
```

This way, our index.html will stay in the src folder together with the input.css from TailwindCSS.

### Vite workflow
Vite looks for *index.html* in *src* folder and starts bundling all external references including *main.js* and *index.css* (from Tailwind).

In main.js we load external javascripts (in this case AlpineJS and Monaco).
Vite will bundle/minify these references.


## TailwindCSS
TailwindCSS has been installed following this guide <https://tailwindcss.com/docs/guides/vite>

TailwindCSS main CSS file is loaded from *main.js* such as:

```javascript
import './input.css'
```

This gets injected into each page as a style tag e.g.:

```html
<link rel="stylesheet" href="/assets/index-17bfadfc.css">
```
TailwindCSS will look for changes in the following files
```json
content: [
    "./src/index.html",
    "./src/**/*.{svelte,js,ts,jsx,tsx}",
  ]
  ```

Please note we are having Vite work from the src folder hence the *./src/index.html* above.

For TailwindCSS there's also a convenient *watch* script in package.json:
```json
"watch": "tailwindcss -i ./src/input.css -o public/main.css --watch"
```
You can use it as:
```cli
npm run watch &
```
To keep TailwindCSS watch for changes and keeping it in background with *&* if necessary.

## AlpineJS
AlpineJS has been installed with 
```cli
npm install alpinejs
```
AlpineJS is simply loaded from the *main.js*.