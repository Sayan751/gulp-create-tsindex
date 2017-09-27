gulp-create-tsindex
===
[![NPM version][npm-image]][npm-url] 

This gulp plugin will join your typescript files into one export file.

## Installation

Install `gulp-create-tsindex` using npm into your local repository.

```bash
npm install gulp-create-tsindex --save-dev
```
## Usage

Extend your typescript gulp task to create a index file.

```js
var gulp = require('gulp');
var ts = require("gulp-typescript");
var tsindex = require('gulp-create-tsindex');

var tsProject = ts.createProject('tsconfig.json');

gulp.task('build-typescript', function () {
	return gulp.src('./src')
		.pipe(tsindex('./src/index.ts'))
		.pipe(ts(tsProject));
		.pipe(gulp.dest('dist'));
});
```
This will create a file `index.ts` and inject it into the typescript build.

Example `index.ts`:
```js
export * from "./file_A";
export * from "./file_B";
export * from "./file_C";
```

### Don't want to expose all files?

You can ignore typescript files to be added in the index, and thereby making the exports in that file "package-scoped". 

To achieve that, use the token `"/// tsindex:ignore"` in the source file, which needs to be ignored. The file content must start with the ignore token, as shown in the example below.

  ```typescript
  /// tsindex:ignore
  import { stuffs } from "somepackage1"
  ...

  export class MyInternalStuffInPackage{
  ...
  }
  ``` 
If you don't like the default token, you can configure it via build task:
  ```javascript
  tsProject.src()
      .pipe(tsindex(paths.src + '/index.ts',{ignoreToken:"/// my_custom_token"}))
      ...
  ```
  Note that this is optional; however, in this case, the token `/// my_custom_token` needs to be used in the source file instead.

  This strategy is too simple for you? Let us know.

## License

[Apache 2.0](/license.txt)

[npm-url]: https://npmjs.org/package/gulp-create-tsindex
[npm-image]: http://img.shields.io/npm/v/gulp-create-tsindex.svg