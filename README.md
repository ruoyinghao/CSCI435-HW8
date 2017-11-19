<h1>HW #8 - Web Development, JavaScript | CSCI435 F17 | College of William and Mary</h1>
<h2>Introduction</h2>
Web development is the process of making web sites for the internet or intranet.
In this tutorial we will be focus on front-end web development.
In front-end web development, HTML handles the layout of the web page, CSS adds 
arts and color to the page, and JavaScript handles user interaction and makes 
the web page change dynamically.
<br />
<br />
In this tutorial you will be making a dynamic web page that lets you view and search for
certain or all Computer Science classes offered at William and Mary in Fall 2017.
You will use AngularJS, which is a JavaScript framework, to create filters for these courses.
<h2>Files</h2>
In this repository you can see the following files
1. index.html: the skeleton HTML file that will house all the code, so far it has no content in it.
2. class.json: the file that stores all Fall 2017 CS class information
3. README.md: This tutorial

<h2>Tutorial</h2>
<h3>Linking AngularJS</h3>
First, in order to let AngularJS run on the web page, you have to make the web page
aware of the presence of AngularJS. A simple way to do this without storing a .js
file locally is to provide HTML with an external link to a script file in a `<script>` tag.
<br />
<br />
To accomplish this, add the following line between the `<head>` tags. Preferably
after the `<title>` tag.
```
<script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.6.6/angular.min.js"></script>
```

<h3>ng-app</h3>
We need to define an AngularJS app in order to run AngularJS by using `ng-app`.
Typically `ng-app` is placed in the root element of the page, so we define the body of the HTML as an "TableFilterApp".
<br />
<br />
Modify the `<body>` tag to the following:
```
<body ng-app="TableFilterApp">
```

<h3>ng-controller</h3>
Another critical AngularJS component is the controller, which controls the application,
and it is defined by the directive `np-controller`. Typically, a controller is responsible
for a single view. We define a controller in the `<body>` tag:
```
<body ng-app="TableFilterApp" ng-controller="TableFilterController">
```
<h3>Display your name</h3>
To make the grading process easier, we require you to display your name on the page.
We need an input box where we can write names. Using AngularJS's data binding functionality
we can have our input displayed instantly on the web page. To do this we need
to define a model that binds the input value with a JavaScript variable, the value of the
variable will be displayed on the page.
To define a model, simply define it in an `<input>` tag:
```
<input type='text' ng-model='inputValue' />
```
<h3>Display your name(the JavaScript part)</h3>
Now let's write the JavaScript that sets the variable that would be displayed on the screen.
In HTML, JavaScript is located in between  `<script>` tags. Place the script in `<head>`.
Sometimes you may want to place the script in a different element,
check out this [stackoverflow answer](https://stackoverflow.com/questions/3531314/should-i-write-script-in-the-body-or-the-head-of-the-html)
to get an idea about where to put a script. 
```
<script>
  angular.module('TableFilterApp', [])
    .controller('TableFilterController', function($scope) {
      $scope.inputValue = "";
     });
  </script>
```

The `inputValue` is null by defult, as the input changes, `inputValue` will also change.
In this code the AngularJS function takes in a `$scope` object as a parameter.
Also, don't forget to put the inputValue next to the input box by writing `Name: {{inputValue}}` next to the `<input>` tag.

<h3>Load JSON</h3>
To generate a table of Computer Science classes and their information, first we need to retrieve the data.
In our tutorial the data is stored locally, in production you will often need to retrieve it from a database
or use a provided API. We use AngularJS's `$http` service to accomplish this.
Add the following to the JavaScript you've written, before:
```
$http.get('class.json')
      .then(function(res){
        $scope.apps=res.data;
      });
```
__The code above should be located below `$scope.inputValue = "";`__

<br />
<br />
You will also need to add `$http` service as a function parameter, so your JavaScript controller
should look like the following:
```
.controller('TableFilterController', function($scope, $http) {
    //already written code
});
```
__Do not just copy and paste this code. We don't need two controllers. Instead, simply__
__add "$http" to the ".controller" line you've written in the last step.__

<h3>Load data into a table</h3>
We have connected JSON file with HTML, now it is time to display them in a table.
The table will have a list of headers, a list of input boxes so that we can search
and apply filters, and, of course, the course information. 
Create an HTML table by writing this code in the body:
```
<table>
<tr>
  <th>CRN</th>
  <th>Course ID</th>
</tr>
<tr>
  <td><input ng-model="f.crn"></td>
  <td><input ng-model="f.courseID"></td>
</tr>
<tr ng-repeat="a in apps | filter:f">
  <td>{{a.crn}}</td>
  <td>{{a.courseID}}</td>
</tr>
</table>
```
This code displays the header CRN and Course ID, two input boxes, and the CRN and Course ID of all CS Classes.
`ng-repeat` iterates over `app`, which contains all the data. `|` in `ng-repeat` indicates a filter. 
By setting `ng-model` in input boxes in this way, we can use the input value as a filter.
<br />
<br />
__Now, modify the code so that it not only displays and filters by CRN and Course ID, but also by course title, instructor, and status.__
__You should inspect the JSON file to determine what keys you should use__
<br />
<br />
After that, you are done!

<h3>View the Web Page</h3>
Throughout the development, you would want to test or view your web page. Refer to the 
following [Google Doc](https://docs.google.com/a/email.wm.edu/document/d/1uV2fBhoYXLCQkSceBKRaa3BZJm_izGwEUrDTAwkV3z4/edit?usp=sharing) on how to view your web page.

__For grading purpose, we ask you to upload the homework to GitHub and let its "GitHub Pages" service host it, the instruction for using "GitHub Page" is included in the Google Doc.__

<h2>References</h2>
When creating this homework we consulted this tutorial: 
[AngularJS: filter table created with ng-repeat](https://code-maven.com/angular-filter-table-created-with-ng-repeat)

Here are some documentations if you want to keep learning about AngularJS:
* [AngularJS Documentation: Concepts](https://docs.angularjs.org/guide)
* [ng-model](https://docs.angularjs.org/api/ng/directive/ngModel)
* [ng-repeat](https://docs.angularjs.org/api/ng/directive/ngRepeat)
* [W3School AngularJS Tutorial](https://www.w3schools.com/angular/default.asp)

