# async-throttle

Throttling made simple, easy, async.

## How to use

This example fetches the `<title>` tag of the supplied websites,
but it processes a maximum of **two at a time**.

<p align="center">
  <img src="https://cldup.com/QstcrynRNT.gif" />
</p>

```js
// deps
const fetch = require('node-fetch')
const createThrottle = require('async-throttle')
const cheerio = require('cheerio').load

// code
const throttle = createThrottle(2)
const urls = ['https://zeit.co', 'https://google.com', /* … */]
Promise.all(urls.map((url) => throttle(async () => {
  console.log('Processing', url)
  const res = await fetch(url)
  const data = await res.text()
  const $ = cheerio(data)
  return $('title').text()
})))
.then((titles) => console.log('Titles:', titles))
```

To run this example:

```
git clone git@github.com:zeit/async-throttle
npm install
async-node example.js
```
