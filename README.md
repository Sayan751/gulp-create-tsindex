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

## License

[Apache 2.0](/license.txt)

[npm-url]: https://npmjs.org/package/gulp-create-tsindex
[npm-image]: http://img.shields.io/npm/v/gulp-create-tsindex.svg