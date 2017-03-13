# showcar-gulp

Unified frontend build pipeline for projects using the ShowCar UI Library

## Install
```
npm install showcar-gulp -D
```

## Before starting

Install gulp

```
npm install gulp -D
```

## Usage

Create your own `gulpfile.js` with the following structure

```js
// gulpfile.js

const gulp = require('gulp');
const scgulp = require('showcar-gulp')(gulp);

// gulp tasks alliases
gulp.task('set-dev', () => {
    scgulp.config.devmode = true;
});

gulp.task('build', [
    'scss',
    'js'
]);

gulp.task('dev', ['set-dev', 'scss:watch', 'js:watch', 'serve']);
gulp.task('default', ['build']);
```

## Build tasks

JS
Build and minify your js files

```js
gulp.task('js', scgulp.js({
    entry: 'src/main.js',
    out: 'dist/main.min.js'
}));
```

SCSS
Build and minify css from sass files

```js
gulp.task('scss', scgulp.scss({
    entry: 'src/main.scss',
    out: 'dist/showcar.min.css'
});
```

## Linter tasks

Tasks for linting JS and CSS code style

JS
```js
gulp.task('eslint', scgulp.eslint({
    files: 'src/**/*.js'
});
```
CSS
```js
gulp.task('stylelint', scgulp.stylelint({
    files: 'src/**/*.scss'
});
```

For running linter tasks you will also need to create configuration files in your project.

`.eslintrc.js` for eslint task

`.stylelintrc.js` for stylelint task


## Serve task
Runs a local server on localhost:3000 by default

```js
gulp.task('serve', scgulp.serve({
    dir: 'dist'
});
```


## Clean task
Removes files according to the `files` pattern

```js
gulp.task('clean', scgulp.clean({
    files: ['dist/**/*']
});
```


## Karma task

Runs karma tests

```js
gulp.task('jstest' scgulp.js({
    entry: 'src/main.spec.js',
    out: 'dist/main.min.spec.js',
    watch: ['test-src/**/*.js', 'js-src/**/*.js'],
});

gulp.task('karma', ['jstest'], scgulp.karma({
    files: ['dist/index.spec.js']
});

gulp.task('jstest:watch', () => {
    gulp.watch(['test-src/**/*.js', 'js-src/**/*.js'], ['karma']);
});
```

<!--### Cross-browser testing on saucelabs

Please note, running tests on saucelabs requires `SAUCE_USERNAME` and `SAUCE_ACCESS_KEY` env variables to be set correctly.

```js
karma: {
    dependencies: ['jstest'],
    files: ['dist/index.spec.js'],
    sauceLabs: {
        startConnect: true
        // all available options are here: https://github.com/karma-runner/karma-sauce-launcher
    }
}
```-->

## Usage example

[Please see our gulpfile](./gulpfile.js)
