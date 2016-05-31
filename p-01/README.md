# Project 1

## Purpose
To learn how to build a fullstack application using Node and Angular.

## Prerequisites
- C9
- JazzHub

## Instructions
Fork this repo:
https://hub.jazz.net/project/chyld/full-stack-template/overview

Clone into C9 ~/workspace directory

Install node modules
- `npm install`

Run pre-made test
- `npm test`

Start server
- `nodemon server/index.js`

Open browser
- http://WORKSPACE-USER.c9users.io/
- Example URL, my workspace is 'bluemix' and user is 'chyld'
- http://bluemix-chyld.c9users.io/

The next 30min to 1hr is essentially an Angular tutorial. After the tutorial, the project will resume.

Open client/index.html and client/index.js. Place files side by side so students can see how they interact.

The HTML file uses Twitter Bootstrap. Go to http://getbootstrap.com/css/ and explain how TB works, its grid system. Show them how TB is used in our code.

Review some basic HTML tags: H1 to H6, P, A, IMG, UL/LI.

Show them how Angular works. Create some properties on `$scope` and show students how those values can be seen in the HTML.
- index.js
```js
angular.module('template', [])
.controller('MainCtrl', function($scope){
  $scope.x = 3;
  $scope.y = "bob";
  $scope.nums = [4,5,6];
});
```

Use the mustache syntax to show them one-way data binding.
- index.html
```html
<div>
  {{x}}
  {{y}}
  {{nums}}
</div>
```

Now show how to loop over an array in HTML. Put in the following code to loop over the `nums` array.
- index.html
```html
<ul ng-repeat="n in nums track by $index">
  <li>Number: {{n}} Squared: {{n*n}}</li>
</ul>
```

Next, let's add a button and input field so that we can dynamically add a value to the array and have it update the HTML automatically.
- index.html
```html
<input type="number" ng-model="num">
<button ng-click="add()">Add</button>
```

The `add` button does nothing, so let's wire it up in the controller.
- index.js
```js
$scope.add = function(){
  $scope.nums.push($scope.num);
};
```
