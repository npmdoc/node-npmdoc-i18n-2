# api documentation for  [i18n-2 (v0.6.3)](http://github.com/jeresig/i18n-node-2)  [![npm package](https://img.shields.io/npm/v/npmdoc-i18n-2.svg?style=flat-square)](https://www.npmjs.org/package/npmdoc-i18n-2) [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-i18n-2.svg)](https://travis-ci.org/npmdoc/node-npmdoc-i18n-2)
#### lightweight simple translation module with dynamic json storage

[![NPM](https://nodei.co/npm/i18n-2.png?downloads=true)](https://www.npmjs.com/package/i18n-2)

[![apidoc](https://npmdoc.github.io/node-npmdoc-i18n-2/build/screenCapture.buildNpmdoc.browser._2Fhome_2Ftravis_2Fbuild_2Fnpmdoc_2Fnode-npmdoc-i18n-2_2Ftmp_2Fbuild_2Fapidoc.html.png)](https://npmdoc.github.io/node-npmdoc-i18n-2/build/apidoc.html)

![npmPackageListing](https://npmdoc.github.io/node-npmdoc-i18n-2/build/screenCapture.npmPackageListing.svg)

![npmPackageDependencyTree](https://npmdoc.github.io/node-npmdoc-i18n-2/build/screenCapture.npmPackageDependencyTree.svg)



# package.json

```json

{
    "author": {
        "name": "John Resig",
        "email": "jeresig@gmail.com"
    },
    "bugs": {
        "url": "https://github.com/jeresig/i18n-node-2/issues"
    },
    "dependencies": {
        "sprintf": "^0.1.5"
    },
    "description": "lightweight simple translation module with dynamic json storage",
    "devDependencies": {
        "expresso": ">=0.9.2",
        "js-yaml": "^3.4.3"
    },
    "directories": {
        "lib": "."
    },
    "dist": {
        "shasum": "57ac6185e3ea47cffe993cd7a5c14b40df364b39",
        "tarball": "https://registry.npmjs.org/i18n-2/-/i18n-2-0.6.3.tgz"
    },
    "engines": {
        "node": ">=0.4.0"
    },
    "gitHead": "b99fd69469d0f014c1a2015800aa206d8ed23998",
    "homepage": "http://github.com/jeresig/i18n-node-2",
    "license": "MIT",
    "main": "./index",
    "maintainers": [
        {
            "name": "gjuchault",
            "email": "gabriel.juchault@gmail.com"
        },
        {
            "name": "jeresig",
            "email": "jeresig@gmail.com"
        },
        {
            "name": "klicher",
            "email": "kristoffer.lr@gmail.com"
        }
    ],
    "name": "i18n-2",
    "optionalDependencies": {},
    "readme": "ERROR: No README data found!",
    "repository": {
        "type": "git",
        "url": "git+ssh://git@github.com/jeresig/i18n-node-2.git"
    },
    "scripts": {
        "test": "expresso test/*"
    },
    "version": "0.6.3"
}
```



# <a name="apidoc.tableOfContents"></a>[table of contents](#apidoc.tableOfContents)

#### [module i18n-2](#apidoc.module.i18n-2)
1.  [function <span class="apidocSignatureSpan">i18n-2.</span>expressBind (app, opt)](#apidoc.element.i18n-2.expressBind)
1.  [function <span class="apidocSignatureSpan">i18n-2.</span>registerMethods (helpers, req)](#apidoc.element.i18n-2.registerMethods)
1.  object <span class="apidocSignatureSpan">i18n-2.</span>localeCache
1.  object <span class="apidocSignatureSpan">i18n-2.</span>resMethods
1.  string <span class="apidocSignatureSpan">i18n-2.</span>version



# <a name="apidoc.module.i18n-2"></a>[module i18n-2](#apidoc.module.i18n-2)

#### <a name="apidoc.element.i18n-2.expressBind"></a>[function <span class="apidocSignatureSpan">i18n-2.</span>expressBind (app, opt)](#apidoc.element.i18n-2.expressBind)
- description and source-code
```javascript
expressBind = function (app, opt) {
	if (!app) {
		return;
	}

	app.use(function (req, res, next) {
		opt.request = req;
		req.i18n = new i18n(opt);

		// Express 3
		if (res.locals) {
			i18n.registerMethods(res.locals, req)
		}

		next();
	});

	// Express 2
	if (app.dynamicHelpers) {
		app.dynamicHelpers(i18n.registerMethods({}));
	}
}
```
- example usage
```shell
...

## API:

### 'new i18n(options)'

The 'i18n' function is the return result from calling 'require('i18n-2')'. You use this to instantiate an 'I18n' instance and set
 any configuration options. You'll probably only do this if you're not using the 'expressBind' method.

### 'i18n.expressBind(app, options)'

You'll use this method to attach the i18n functionality to the request object inside Express.js. The app argument should be your
 Express.js app and the options argument should be the same as if you were calling 'new i18n(options)'. See **"Using with Express
.js"** at the end of this README for more details.

### '__(string, [...])'

Translates a string according to the current locale. Also supports sprintf syntax, allowing you to replace text, using the node-
sprintf module.
...
```

#### <a name="apidoc.element.i18n-2.registerMethods"></a>[function <span class="apidocSignatureSpan">i18n-2.</span>registerMethods (helpers, req)](#apidoc.element.i18n-2.registerMethods)
- description and source-code
```javascript
registerMethods = function (helpers, req) {
	i18n.resMethods.forEach(function (method) {
		if (req) {
			helpers[method] = req.i18n[method].bind(req.i18n);
		} else {
			helpers[method] = function (req) {
				return req.i18n[method].bind(req.i18n);
			};
		}

	});

	return helpers;
}
```
- example usage
```shell
n/a
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)
