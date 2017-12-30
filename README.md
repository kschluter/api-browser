# API Browser

> Single page VueJS app for browsing publicly available APIs


# Motivations
I developed this app mostly as an ongoing testbed for my NPM module <a href="https://github.com/kschluter/vue2ghp">vue2ghp</a> which easily builds and deploys VueJS CLI generated apps (such as this one) to GitHub pages. I also wanted an easy way to browse/filter/sort a listing of publicly available APIs.

# Libraries in Use
* <a href="https://github.com/vuejs/vue">VueJS</a>
* <a href="https://github.com/ElemeFE/element">ElementUI</a>
* <a href="https://github.com/njleonzhang/vue-data-tables">DataTables</a>
* <a href="https://github.com/kschluter/vue2ghp">vue2ghp</a>

# Usage

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build

# deploy to GitHub Pages (Switch homepage key in your package.json to point to your own repo)
npm run deploy
```
# Credits
This app uses the fetch API to import raw JSON data from Todd Mottos' <a href="https://github.com/toddmotto/public-apis">public-apis</a> repo.

# License
MIT
