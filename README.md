# parse-appcache-manifest [![Build Status](https://travis-ci.org/meryn/parse-appcache-manifest.png?branch=master)](https://travis-ci.org/meryn/parse-appcache-manifest) [![Dependency Status](https://david-dm.org/meryn/parse-appcache-manifest.png)](https://david-dm.org/meryn/parse-appcache-manifest)

Parses HTML5 application cache manifest.

## Usage

`npm install parse-appcache-manifest`

#### Direct Object

```javascript
parseManifest = require("parse-appcache-manifest")
entries = parseManifest(manifest)
```

`entries` will be an object with four properties: `cache`, `network`, `fallback`, and `settings`. 

`cache`, `settings`, and `network` are arrays which contain entries. 

`fallback` is an object with the url (or url pattern) as key, and the fallback url as value.


#### Tokenized
If you need access to a tokenized version of the manifest file (e.g., you want to modify an existing manifest file and need to preserve comments and newlines, etc)


```coffeescript
appcacheParse  = require 'parse-appcache-manifest'
result = appcacheParse(input).tokens
```

where `result` is a flat, ordered list of tokens that comes back. 

 `input` =

```
CACHE MANIFEST

# some explicit resources
CACHE:
/happy.html
/good.css

NETWORK:
*
http://*
https://*
```

`result` =

```json
[
  { type: 'magic signature', value: 'CACHE MANIFEST' },
  { type: 'newline' },
  { type: 'comment', value: 'some explicit resources' },
  { type: 'mode', value: 'CACHE' }
  { type: 'data', tokens: [ '/happy.html' ] },
  { type: 'data', tokens: [ '/good.css' ] },
  { type: 'newline' },
  { type: 'mode', value: 'NETWORK' }
  { type: 'data', tokens: [ '*' ] },
  { type: 'data', tokens: [ 'http://*' ] },
  { type: 'data', tokens: [ 'https://*' ] }
]
```

You can use https://github.com/meryn/render-appcache-manifest to convert a token list back to an appcache manifest.

## Development

To compile the code:

```sh
cd parse-appcache-manifest
coffee -cm -o lib/ src/
```

## Credits

The initial structure of this module was generated by [Jumpstart](https://github.com/meryn/jumpstart), using the [Jumpstart Black Coffee](https://github.com/meryn/jumpstart-black-coffee) template.

This code is based on code from [Mikko Ohtamaa](http://opensourcehacker.com/).

Tokenizing support, settings support, whatwg spec conformance, and updated documentation from https://github.com/mreinstein.

## License

parse-appcache-manifest is released under the [MIT License](http://opensource.org/licenses/MIT).  
Copyright (c) 2013 Meryn Stol  