# ***Gulp***

### Gulp Command
[gulp-command](https://www.npmjs.com/package/gulp-command)

`gulp.option('<related-task>', '-f, --flag', 'Description', 'callback')`
- Related-Task: optional If No Related task is specified, the commands can apply to all tasks, but you must add `null`
- -f, --flag: required (both short and long flag are required comma Separated)
- Description: required
- Callback: optional

Run `gulp build -e` /// logs e: true ***Default***

Run `gulp build -e=production` /// logs e: 'production'  ***Equal to Something***
``` javascript
'use strict';
const gulp = require('gulp');
require('gulp-command')(gulp);

gulp.option(null, '-e, --env', 'Awesome Thing')
.option(null, '-p, --production', 'So Totally Cool')
.task('build', () => {
  .pipe(gulpif(this.flags.env, 'trust'))
  console.log(this.flags); // { production: undefined, env: 'production' }
  console.log(!this.flags.production && !this.flags.env ? 'true' : 'false'); // false
});
```

### Gulp If
- [gulp-if](https://www.npmjs.com/package/gulp-if)

Running `gulp build -e` will pipe uglify. Because this.flags.env will equal true.

``` javascript
const gulp = require('gulp');
require('gulp-command')(gulp);
const gulpif = require('gulp-if');
const uglify = require('gulp-uglify');

const JS_DIRECTORY = 'dev/js/**/*.js';

gulp.option(null, '-e, --env', 'Awesome Thing')
.option(null, '-p, --production', 'So Totally Cool')
.task('js', () => {
  gulp.src(JS_DIRECTORY)
  .pipe(gulpif(this.flags.env, uglify()))
  .pipe(gulp.dest('dist/js'))
});
```

### Gulp Build
[gulp-build](https://www.npmjs.com/package/gulp-build)

`gulp-build` uses HandleBars for templates, and supports helpers, partials, and layouts.

``` javascript
const gulp = require('gulp');
const build = require('gulp-build');

const HTML_DIRECTORY = './public/index.html';

gulp.task('html', () => {
  gulp.src(HTML_DIRECTORY)
  .pipe(gulpBuild({ message: !this.flags.production && !this.flags.env ? 'hi' : 'bye' }))
  .pipe(gulp.dest('./public'))
});
```

```html
<!DOCTYPE html>
<html lang="en">
<head></head>
<body>
  <div id="app">
    <h1>{{message}}</h1><!-- <h1>Some page</h1> -->
  </div>
</body>
</html>
```

### Gulp Sourcemaps
[gulp-sourcemaps](https://www.npmjs.com/package/gulp-sourcemaps)

Allows you to view the uncompiled file in the dev tools.

Pipe `sourcemaps init` first and then after piping all filters pipe `sourcemaps write(.)` this will drop a css map file. I.E. `styles.css.map`

``` javascript
const gulp = require('gulp');
const uglify = require('gulp-uglify');
const sourcemaps = require('gulp-sourcemaps');

const JS_DIRECTORY = 'dev/js/**/*.js';

gulp.task('js', () => {
  gulp.src(JS_DIRECTORY)
  .pipe(sourcemaps.init())
  .pipe(uglify())
  .pipe(sourcemaps.write('.'))
  .pipe(gulp.dest('dist/js'))
});
```

### Gulp Plumber & Gulp Notify
- [gulp-plumber](https://www.npmjs.com/package/gulp-plumber)
- [gulp-notify](https://www.npmjs.com/package/gulp-notify)

`gulp-plumber` prevents gulp from [failing](https://nodejs.org/api/process.html#process_event_uncaughtexception) when error occurs and `gulp-notify` makes an error message & sound notification.
``` javascript
const gulp = require('gulp');
const plumber = require("gulp-plumber");
const notify = require("gulp-notify");
const scss = require('gulp-sass');

const SCSS_DIRECTORY = 'dev/scss/**/*.scss';

gulp.task('scss', () => {
  gulp.src(SCSS_DIRECTORY)
  .pipe(plumber({
    errorHandler: notify.onError("Error: <%= error.message %>")
  }))
  .pipe(scss())
  .pipe(gulp.dest('dist/css'))
});
```

### Gulp Live Server
- [gulp-live-server](https://www.npmjs.com/package/gulp-live-server#stop)

Run Express server in Gulp.

``` javascript
const gls = require('gulp-live-server');
const server = gls.static('./public', 3000);
server.start();
```
