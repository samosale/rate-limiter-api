# <a id="app-top"></a> Rate Limiter API

[![Rate Limiter API image](http://i.imgur.com/JDFpgQZ.jpg "Rate Limiter API image")](#app-top)

[![All Contributors](https://img.shields.io/badge/all_contributors-1-orange.svg?style=flat-square)](#contrib) [![MIT License](https://img.shields.io/badge/License-MIT-56A902.svg?style=flat-square&maxAge=2592000)](LICENSE)  
A library to easily manage rate limits of API without any hassle.

## <a id="toc"></a> Table of Contents
- [How to Use](#usage)
 - [Browser](#usage-browser)
 - [NodeJS](#usage-nodejs)
- [Public API](#public-api)
- [Stats](#stats)
- [Technologies Used](#techs)
- [Help & Support](#help)
- [Contributors](#contrib)
- [License](#license)
- [Contact](#contact)


## <a id="usage"></a>Usage <a href="#toc" title="Table of Contents"><kbd>⮭</kbd></a>
#### <a id="usage-browser"></a>Browser <a href="#toc" title="Table of Contents"><kbd>⮭</kbd></a>
```html
<script src="https://cdn.rawgit.com/abhisekp/rate-limiter-api/master/dist/rate-limiter-api.js"></script>
```

#### <a id="usage-nodejs"></a>NodeJS <a href="#toc" title="Table of Contents"><kbd>⮭</kbd></a>
```sh
$ {sudo -H} npm install -S rate-limiter-api
```

```js
import RateLimiterAPI from 'rate-limiter-api'
```


## <a id="public-api"></a>Public Interface <a href="#toc" title="Table of Contents"><kbd>⮭</kbd></a>
- `rl = RateLimiterAPI({threshold: 5})`
- `rl.limit(requestHandler) => Promise`
 - `rl.updateRateLimits` on success to update rates
 - `requestHandler(responseHandler)` on success to continue

----
```js
import RateLimiterAPI from 'rate-limiter-api'

const rl = RateLimiterAPI({
  threshold: 5, // leave `threshold` amount of api requests intact (minimum: 1)
})
```

Pass an optional `threshold` value which would limit the total rate limits till the threshold is reached in the current session pulse till rate reset.

----
```js
const request = rl.limit(requestHandler) //=> Promise

function requestHandler(responseHandler) {
  fetch('https://api.example.com/get')
    .then((response) => {
      rl.updateRateLimits({
        rateLimit: response.headers.rateLimit,
        rateRemaining: response.headers.rateRemaining,
        rateReset: response.headers.rateReset,
      })

      responseHandler(null, response.body)
    })
    .catch((err) => {
      responseHandler(err)
    })
}
```

The `limit` method is passed a `requestHandler` which would manage the request and then call the node-style `responseHandler` callback (which gets passed by the RateLimiter library to the `requestHandler` function) after the request is successful or unsuccessful accordingly.

The `request` method returns a `Promise`.

> responseHandler(Error, response)  
where the first parameter is the Error object and the seconds parameter is the `response`.

`responseHandler` callback must be called to continue getting responses.

Update the rate limits i.e. `{rateLimit, rateRemaining, rateReset}` got from the header using `updateRateLimits` method.

----
```js
request
  .then((response) => {
    console.dir(response, {colors:1})
  })
  .catch((error) => {
    console.error(error.message)
  })
```

When the request completes, the `Promise` resolves and can be thenable to get the response or error.

## <a id="stats"></a>Stats <a href="#toc" title="Table of Contents"><kbd>⮭</kbd></a>

1 text file.  
1 unique file.  
0 files ignored.  

https://github.com/AlDanial/cloc v 1.66  T=0.04 s (22.7 files/s, 2516.9 lines/s)

Language|files|blank|comment|code
:---|:---:|:---:|:---:|:---:
JavaScript|1|12|37|62


## <a id="techs"></a>Technologies Used <a href="#toc" title="Table of Contents"><kbd>⮭</kbd></a>
- [**Babel**](http://babeljs.io) — Transpiles modern JS to compatible and runnable JS
- [**Stamp It**](https://github.com/stampit-org/stampit#readme) - Composable inheritance object creation libray
- [**Async JS**](https://caolan.github.io/async/index.html) - Utility for asynchronous functions
- [**Lodash**](https://lodash.com/) - Utility library

## <a id="help"></a>Help & Support <a href="#toc" title="Table of Contents"><kbd>⮭</kbd></a>
- [**BabelJS**](https://babeljs.slack.com) — BabelJS Slack Chat Room
- [**nodejs/node**](https://gitter.im/nodejs/node) — NodeJS Gitter Chat Room
- [**Fun with Stamps**](https://medium.com/@koresar/fun-with-stamps-episode-1-stamp-basics-e0627d81efe0) - Learn StampIt


## <a id="contrib"></a>Contributors <a href="#toc" title="Table of Contents"><kbd>⮭</kbd></a>

<!-- ALL-CONTRIBUTORS-LIST:START - Do not remove or modify this section -->
| [![Abhisek Pattnaik](https://avatars.githubusercontent.com/u/1029200?v=3&s=100)<br /><sub>Abhisek Pattnaik</sub>](http://about.me/abhisekp)<br />[💻](https://github.com/abhisekp/Practice-Modern-JavaScript/commits?author=abhisekp) 🎨 [📖](https://github.com/abhisekp/Practice-Modern-JavaScript/commits?author=abhisekp) 💡 |
| :---: |
<!-- ALL-CONTRIBUTORS-LIST:END -->
This project follows the [all-contributors](https://github.com/kentcdodds/all-contributors#emoji-key) specification.

> **All types of Contributions are Welcome** :pray:

## <a id="license"></a>License <a href="#toc" title="Table of Contents"><kbd>⮭</kbd></a>

[**MIT**](LICENSE) © [**Abhisek Patnaik**](https://github.com/abhisekp)

> ----
<a id="contact"></a>
<p align="center">
Tweet <kbd><a href="https://twitter.com/abhisek"><b><img src="https://i.imgur.com/wOPZd0Y.png?1"> @abhisek</b></a></kbd><br>
Know <kbd><b><a href="https://about.me/abhisekp">about/abhisekp</a></b></kbd><br>
Chat with <kbd><a href="https://gitter.im/abhisekp">
<img src="https://i.imgur.com/ThSWa6Y.png?2"> <b>@abhisekp</b></a></kbd>
</p>

> ----

<div align="right">
 <a href="#toc" title="Table of Contents"><kbd><b>Table of Contents ⮭</b></kbd></a><br>
 <a href="#app-top"><kbd><b>back to top ⮭</b></kbd></a>
</div>
