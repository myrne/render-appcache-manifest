# render-appcache-manifest [![Build Status](https://travis-ci.org/meryn/render-appcache-manifest.png?branch=master)](https://travis-ci.org/meryn/render-appcache-manifest) [![Dependency Status](https://david-dm.org/meryn/render-appcache-manifest.png)](https://david-dm.org/meryn/render-appcache-manifest)

Renders HTML5 application cache manifest.

See also [parse-appcache-manifest](http://npmjs.org/package/parse-appcache-manifest).

## Usage

`npm install render-appcache-manifest`

#### Generate Manifest from Direct Object
```javascript
renderManifest = require "render-appcache-manifest"
renderManifest(contents)
```

`renderManifest` returns the rendered manifest as a string.  
`contents` is an object that can have the following properties, all optional:

* `cache` - an array of entries (urls) you want in the `CACHE` section.
* `network` - an array of entries (urls or url-patterns, using wildcards) you want in the `NETWORK` section
* `fallback` - an object with key-value pairs where key is the url or url-pattern to capture, and value is the fallback url. They will appear in the `FALLBACK` section.
* `settings` - an array of settings. Currently the only value that appcaches understand is `prefer-online` or `fast` which refers to the caching mode enabled. See http://www.whatwg.org/specs/web-apps/current-work/multipage/offline.html#parsing-cache-manifests for full details.
* `unique` - if set to a truthy value, will add result of `Math.random()` as a comment, guaranteeing uniqueness.
* `lastModified` - a `Date` object. Will be used to generate a "Last modified at" comment.
* `comment` - a comment string.
* `comments` - an array of comment strings, each comment will take up one line.

There's no way to control layout of the generated manifest. The output will be generally neat.

render-appcache-manifest will not validate the correctness of input. You are responsible for providing corrent urls or url-patterns, where appropriate. Also, adding a multi-line string as a comment will break the manifest.

#### Generate Manifest from Tokens

If you need fine grained control over the rendering process, you may pass in a list of ordered tokens to render a manifest. The tokens are generated by https://github.com/meryn/parse-appcache-manifest, but you can just as easily craft your own token list provided the format matches.


```coffeescript
appcacheRender = require 'render-appcache-manifest'
out = appcacheRender tokens
```

## Development

To compile the code:

```sh
npm install # once, to get the dev dependencies
make build
```

To test the code:

```sh
npm test
```

## Credits

The initial structure of this module was generated by [Jumpstart](https://github.com/meryn/jumpstart), using the [Jumpstart Black Coffee](https://github.com/meryn/jumpstart-black-coffee) template.

Tokenizing support, settings support, whatwg spec conformance, and updated documentation from https://github.com/mreinstein.

## License

render-appcache-manifest is released under the [MIT License](http://opensource.org/licenses/MIT).  
Copyright (c) 2013 Meryn Stol, [Michael Reinstein](https://github.com/mreinstein)