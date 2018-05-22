# README #

FlexBox has changed over the years.

https://css-tricks.com/old-flexbox-and-new-flexbox/

For example, see the history listed here as it mentions how flex-basis usaged was changed as they were developing the standard:

https://developer.mozilla.org/en-US/docs/Web/CSS/flex-basis

We write our flex box with the cleanest, latest and run it through and autoprefixer.

You can directly paste CSS code into the autoprefixer, and it will transpose it to use all of the various browswer specific usages of FlexBox making your CSS compatible with any browser that ever supported FlexBox ...

https://autoprefixer.github.io/

However, a build step will automatically keep track of changes made to CSS. We will use Gulp.

First, make sure you have Node installed. And you need a pacakge.json file to track package dependencies. To create this file, CD to your project directory, 

```
$ npm init
```

Just accept all of the defaults, and then add this to a simple package.json file:

```
$ cat package.json 
{
  "name": "whatever_directory",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "",
  "license": "ISC"
}
```

Next, install Gulp globally ...


```
sudo npm install gulp -g
```

Next, install the gulp file, which describes the configuration which tells gulp what to do. Start by creating an empty gulp file (again, still in the project directory)

```
touch gulpfile.js
```

Next, we install a local copy of gulp

```
npm install gulp --save-dev
```

Note that if you look in the package.json file, you should see a new entry for "gulp". Next, do this:

```
npm install gulp-autoprefixer --save-dev
```

Which likewise should add an entry in package.json for gulp-autoprefixer. Now edit the gulpfile.js, and add the following code:

```
var gulp = require('gulp');
var autoprefixer = require('gulp-autoprefixer');

gulp.task('styles', function() {
	// gulp.src('css/**/*.css').pipe(autoprefixer()).pipe(gulp.dest('build'));*/
	gulp.src('css/*.css').pipe(autoprefixer()).pipe(gulp.dest('build'));
});
```

Also, enter this in the package.json file (I entered it at the end)

```
,
  "browserslist": [
      "> 1%",
      "last 2 versions"
    ]
```

Now go back to the command line, and enter this:

```
$ gulp styles
```

To add a watch task to gulp, add this new task to the gulpfile.js

```
gulp.task('watch', function() {
	gulp.watch('css/style.css', ['styles']);
});
```

Note that the ['styles'] is the name of the task entered first in the gulpfile.js.

Now go back to the command line and do this:

```
$gulp watch
```

Now every time you save the css/style.css, it will automatically build the build/style.css file