PostCSS HTML Syntax
====

[![NPM version](https://img.shields.io/npm/v/postcss-html.svg?style=flat-square)](https://www.npmjs.com/package/postcss-html)
[![Travis](https://img.shields.io/travis/gucong3000/postcss-html.svg)](https://travis-ci.org/gucong3000/postcss-html)
[![Coverage Status](https://img.shields.io/coveralls/gucong3000/postcss-html.svg)](https://coveralls.io/r/gucong3000/postcss-html)

<img align="right" width="95" height="95"
     title="Philosopher’s stone, logo of PostCSS"
     src="http://postcss.github.io/postcss/logo.svg">

[PostCSS](https://github.com/postcss/postcss) Syntax for parsing HTML

> [vue component](https://vue-loader.vuejs.org/) compatible

## Getting Started

First thing's first, install the module:

```
npm install postcss-html --save-dev
```

If you want support SCSS/SASS/LESS/SugarSS syntaxh, you need to install the corresponding module.

- SCSS: [PostCSS-SCSS](https://github.com/postcss/postcss-scss)
- SASS: [PostCSS-SASS](https://github.com/aleshaoleg/postcss-sass)
- LESS: [PostCSS-LESS](https://github.com/shellscape/postcss-less)
- SugarSS: [SugarSS](https://github.com/postcss/sugarss)

## Use Cases

```js
var syntax = require('postcss-html');
postcss(plugins).process(source, { syntax: syntax }).then(function (result) {
	// An alias for the result.css property. Use it with syntaxes that generate non-CSS output.
    result.content
});
```

### Style Transformations

The main use case of this plugin is to apply PostCSS transformations directly to HTML source code. For example, if you ship a theme written in style tag in HTML and need [Autoprefixer](https://github.com/postcss/autoprefixer) to add the appropriate vendor prefixes to it; or you need to lint style source in HTML with a plugin such as [Stylelint](http://stylelint.io/).

### Inferring the syntax of style file

When passing a non-HTML file, this plugin will infer the syntax by file extension, and fallback by standard CSS syntax.

### Custom unknown syntax

```js
var syntax = require('postcss-html');
postcss(plugins).process(html, {
	syntax: syntax((opts, lang) => {
		if ('stylus' === lang) {
			// Custom syntax by attribute of <style> tag
			return require('postcss-stylus')
		} else if (/\.styl$/.test(opts.from)) {
			// Custom syntax by file extension
			return require('postcss-stylus')
		}
	})
}).then(function (result) {
    result.content
});
```
