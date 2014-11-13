angular-c3    [![Build Status](https://travis-ci.org/maseh87/c3-chart.svg?branch=master)](https://travis-ci.org/maseh87/c3-chart)   <img src="http://img.shields.io/badge/Built%20with-Gulp-red.svg" />
===============

### A simple way to add custom C3 charts to your angular apps. Charts based off [C3](http://c3js.org/).

## Dependencies
+ Angular.js (1.2+)
+ C3js
+ D3js

## Downloading
1. The best way to install angular-c3 is to use bower
    + ```bower install angular-c3 --save```
2. Or, from this repo
  + you'll need the main files in ```dist/```

## Using
+ angular-c3 comes pre-packaged with c3 and d3. No need to download those libraries.
+ Adding a C3 chart is as simple as adding the c3-chart directive to your HTML. Add an id to tell the chart which element to bind to. Also add the config attribute to point to the data inside your controller.

```html
<c3-chart id="chart" config="config"></c3-chart>
```

```javascript
angular.module('chartApp', ['angular-c3'])
.controller('ChartController', function($scope){
  $scope.config = {
    data: {
      x: 'x',
      columns: [
          ['x', '2012-12-29', '2012-12-30', '2012-12-31'],
          ['data1', 230, 300, 330],
          ['data2', 190, 230, 200],
          ['data3', 90, 130, 180],
      ]
    },
    axis: {
        x: {
            type: 'timeseries',
            tick: {
                format: '%m/%d',
            }
        }
    }
  };
});
```

+ To gain access to the chart object inject the c3Factory into the service you need it. Use the .get method to select which chart to select or use the .getAll method to gain access to all c3-charts.

```javascript
.controller('ChartController', function($scope, c3Factory) {
  c3Factory.get('chart').then(function(chart) {
    chart.load({
        columns: [
            ['data1', 30, 200, 100, 400, 150, 250, 50, 100, 250]
            ['data2', 50, 25, 133, 46, 693, 345, 34, 14, 55]
        ]
    });
  });
})
```

##Contributing
1. Fork it
2. Clone your fork
3. Create new branch
4. Make changes
5. Make test and check test
6. Build it, run ```gulp``` and the files will be linted, concatenated, and minified
7. Push to new branch on your forked repo
8. Pull request from your branch to angular-c3 master

###Format for pull request
+ Pretty standard
  + in your commit message; ```(type) message [issue # closed]```
    + ```(bug) killed that bug, closes #45```
+ Submit issues as you see them. There are probably better, faster, easier ways to achieve what angular-c3 is designed to do so.

###Testing
+ angular-c3 uses Karma + Mocha + Travis for unit and ci
+ Make sure you didn't break anything
  + run ```karma start``` to test in Chrome with karma
+ Features will not be accepted without specs created for them
+ Run ```gulp watch``` and all the source files will be watched and concatenated
+ Open the ```index.html``` and use the test app as a playground
