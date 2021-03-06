# Package.json

---

`spm` use the exactly same file `package.json` as `npm` to describe a package, which shares most fileds, except an extra `spm` filed for containing some custom attributes.

### Fields

Field | Description |
------------ | ------------- |
name* | name of the package in lowercase, use a `-` or `.` as a separator between words
version* | semantic versioning like 1.0.0
description | a brief description of the package
keywords | an array of keywords
homepage | url of the package's website
author | author of the package: `Hsiaoming Yang <me@lepture.com>` or `{ "name": "Hsiaoming Yang", "email": "me@lepture.com" }`
maintainers | an array of maintainers, just like author
repository | specify the place where the code is hosted. `{ "type": "git", "url": "http://github.com/isaacs/npm.git" }`
bugs | the url to the package's issue tracker and / or the email address to which issues should be reported.
license | license
**spm*** |
spm.main | the only entry point of the package, default `index.js`, or could be set to `index.css` for a css-only package 
spm.output | an array of other files needed to be output
spm.dependencies | specify dependencies relation of the package
spm.devDependencies | specify dependencies relation of the package in developing situation
spm.tests | specify all test files, support glob patterns: `tests/*-spec.js`
spm.build | specify the cli arguments for `spm build`
spm.ignore | an array of ignore files in package, same function as `.spmignore`
spm.scripts | like npm.scripts, handle around some spm commands, it support `prebuild`, `postbuild`, `preinstall`, `postinstall`, `prepublish`, `postpublish`.  `Not recommend to use!`


### A basic example

```json
{
  "name": "arale-calendar",
  "version": "1.1.0",
  "description": "Calendar widget.",
  "keywords": [
    "widget",
    "month",
    "datepicker"
  ],
  "author": "Hsiaoming Yang <me@lepture.com>",
  "maintainers": [
    "hotoo <hotoo.cn@gmail.com>",
    "shengyan <shengyan1985@gmail.com>"
  ],
  "homepage": "http://aralejs.org/calendar/",
  "repository": {
    "type": "git",
    "url": "https://github.com/aralejs/calendar.git"
  },
  "bugs": {
    "url": "https://github.com/aralejs/calendar/issues"
  },
  "license": "MIT",
  "spm": {
    "main": "calendar.js",
    "dependencies": {
      "jquery": "1.7.2",
      "moment": "2.6.0",
      "arale-base": "1.1.0",
      "arale-position": "1.1.0",
      "arale-iframe-shim": "1.1.0",
      "handlebars": "1.3.0",
      "arale-widget": "1.2.0"
    },
    "devDependencies": {
      "expect.js": "0.3.1"
    },
    "tests": "tests/*-spec.js",
    "ignore": ["dist"],
    "build": {
      // -- Dependency resolution
      // Specify the module or the file does not to be resolved
      "global": {
        "react": "React",
        "./a": "AAA"
      },

      // To enable or disable the node module polyfills
      "node": {
        "global": false
      },

      // -- Performance
      // Extraction Dependencies as vendor.js
      "vendor": ["jquery", "underscore"],
      // Extraction public chunk as common.js
      "common": true,
      "base64": {},

      // -- For other useful js libraries
      "babel": {},
      "uglify": {},
      "autoprefixer": {},
      "less": {},
      "coffee": {},
      "jsx": {},
      "handlebars": {},

      // -- output entries
      "dest": "./build",
      "hash": true,
      // extract css files which js files depend on , the css file name is same to the js file which specified in output field
      "extractCSS": true,
      // Output package names
      "library": "",
      // ex. this, umd, common, amd, var ...
      "libraryTarget": "",
      // equivalent to libraryTarget: umd, library: Foo
      "umd": "Foo",

      //expander  , same to the webpack loader
      "loader": {
        ".js": "+jsdc-babel"
      },

      // use for debugging
      "define": {
        "DEBUG": false
      }
    },
    "scripts": {
      // Not recommend to use!
      "prepublish": "lessc index.less index.css"
    }
  }
}
```
