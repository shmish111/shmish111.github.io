---
layout: post
title: "Configuring REST API endpoint in angular"
description: ""
category:
tags: []
---
{% include JB/setup %}
I've been slowly plodding away learning javascript and the associated ecosystem recently and I have to say the speed with which the community develops new tools and libraries is awesome.  I'm not really a big fan of javascript as a language but it is fun writing an Angular JS app.  The trouble with this speed though is that documentation and examples tend to be a bit thin on the ground, hence this post which can hopefully help someone in a similar situation.

You have a single page Angular JS app which is backed by a RESTfull API.  You would like to be able to run the app without the API service running, using just dummy data.  I think there's probably an infinite number of ways to do this with angular and I went through quite a few of them but here is what I found worked best for my situation.

* Services that interact with the API use a wrapper service around $http
* The wrapper service simply adds a prefix to the url using an angular variable
* The app has 2 versions, the prod app and the dev app which extends the prod app
* The root of the API is set in prod app and overridden in the dev app
* The app then contains a static resource structure, nested folders containing json in files.  As a side-effect this will indicate just how 'RESTfull' my service is!
* The static resources and dev app are included only in the dev build in Gulp
* The ng-app value in index.html is set in the Gulp build using gulp-template

Here's the code

`app/services.js`

    services.service('ApiService', ['$http', 'apiPrefix', function($http, apiPrefix) {
      this.get = function(url) {
        return $http.get(apiPrefix + url);
      };
      this.post = function(url, data) {
        return $http.post(apiPrefix + url, data);
      };
      this.put = function(url, data) {
        return $http.put(apiPrefix + url, data);
      };
    }]);

    services.service('EmailsService', ['ApiService', function(ApiService) {
      this.get = function(id) {
        return ApiService.get('/emails/' + id);
      };
    }]);

`app/app.js`

This is the production version of the angular app

    var app = angular.module('myApp', []);
    ...other app config...
    app.value('apiPrefix', "http://localhost:8080");

`app/app-dev.js`

This is the dev version of the app.  It takes the prod app as a module and extends it.

    var app = angular.module('myAppDev', ['myApp'])
      .value('apiPrefix', "http://localhost:5000");

`app/index.html`

    <html lang="en" ng-app="<%= appName %>">
    ...the rest of the index html...
    </html>

`Gulpfile.js`

    ...gulp imports...
    var browserify = require('gulp-browserify');
    var template = require('gulp-template');

    ...lots of other gulp stuff goes here...

    function doBrowserify(appSrc, appName) {
      gulp.src([appSrc])
      .pipe(browserify({
        insertGlobals: true,
        debug: true,
        transform: ['debowerify']
      }))
      .pipe(concat('bundle.js'))
      .pipe(gulp.dest('dist/js'));

      gulp.src('app/index.html')
            .pipe(template({appName: appName}))
            .pipe(gulp.dest('dist'));
    };

    gulp.task('browserify', function() {
      doBrowserify('app/scripts/app.js', 'myApp');
    });

    gulp.task('dev-browserify', function() {
      doBrowserify('app/scripts/app-dev.js', 'myAppDev');
    });

    // Add some static test data that can be used in place of a real REST service
    gulp.task('testdata', function() {
      gulp.src('app/testdata/**')
      .pipe(gulp.dest('dist'))
      .pipe(refresh(lrserver));
    });

`app/testdata/emails/1` (note this file has no extension, it is simply called '1')

    {
      "to": "some@ddress.com",
      "subject": "hello"
    }

And that's it!  Now my app can be used by simply serving from a static web server, this will also be good for testing as I know exactly what data will be available.
