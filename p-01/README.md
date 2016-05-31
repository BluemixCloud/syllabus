# Project 1

## Purpose
To learn how to build a fullstack application using Node and Angular. This application will fetch the top games from the Twitch API and display them along with their box art on the HTML page.

## Prerequisites
- C9
- JazzHub

## Code
- https://github.com/BluemixCloud/Project-01

## Instructions
Fork this repo:
`https://hub.jazz.net/project/chyld/full-stack-template/overview`

Clone into C9 `~/workspace` directory

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

Now the student can add as many numbers to the array as they like.

This is the end of the Angular tutorial. Let's resume the project.

Have students go to https://api.twitch.tv/kraken/games/top. They can see the JSON returned from the API. They will have Angular fetch this data from the click of a button and then display the Name and Box Art.

Add a button to fetch the data. Also change the page title and description.
- index.html
```html
<div class="row">
  <div class="col-xs-12">
    <h1>Top Games from Twitch</h1>
  </div>
</div>

<div class="row">
  <div class="col-xs-12">
    <button ng-click="twitch()">Get Games</button>
  </div>
</div>
```

The button does nothing, so wire it up in the JS file. Remember to inject `$http` in the controller's function. Log out the response to ensure the data is coming back and to note the structure of the data.
- index.js
```js
angular.module('template', [])
.controller('MainCtrl', function($scope, $http){
  $scope.twitch = function(){
    $http.get('https://api.twitch.tv/kraken/games/top')
    .then(function(rsp){
      console.log(rsp);
    });
  };
});
```

Note the array is under `rsp.data.top`. Create a property on `$scope` that refers to this data.
- index.js
```js
angular.module('template', [])
.controller('MainCtrl', function($scope, $http){
  $scope.twitch = function(){
    $http.get('https://api.twitch.tv/kraken/games/top')
    .then(function(rsp){
      $scope.games = rsp.data.top;
    });
  };
});
```

Now the data is ready. All that is left is to loop over the `games` array in the HTML file and display the name and box art for each game.
- index.html
```html
<div class="row">
  <div class="col-xs-4">
    <table class="table table-striped">
      <thead>
        <tr>
          <th>Name</th>
          <th>Art</th>
        </tr>
      </thead>
      <tbody>
        <tr ng-repeat="game in games">
          <td>{{game.game.name}}</td>
          <td><img src="{{game.game.box.small}}"></td>
        </tr>
      </tbody>
    </table>
  </div>
  <div class="col-xs-4"></div>
  <div class="col-xs-4"></div>
</div>
```

If all works, then ready to deploy.

Edit the `manifest.yml` file, changing the `host` and `path` to a unique value.

Commit and push all changes to JazzHub.

Push app to Cloud Foundry.

`cf push`

Wait for app to deploy, then test out in production.

Project complete.
