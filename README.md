# angular-legacy-sortable
Angular 1.x wrapper for [SortableJS](https://github.com/RubaXa/Sortable). 

### Usage

Add **[ng-sortable]** directive to the parent container of a list of sortable items displayed using **ng-repeat**. The directive will create a SortableJS instance for allowing the child items to be moved inside the container.

When an item is moved to a new position, the original array provided (ng-repeat source) will be modified and reordered according to the new item position.

**Important:** if the ng-repeat source is dynamic or is a reference to a filtered list (using either $filter or an ES6 filter function), it's recommended to use the **onUpdate** option callback to manually reorder your original array. See below for more information on options usage.

```html
<div ng-app="myApp" ng-controller="demo">
	<ul ng-sortable>
		<li ng-repeat="item in items">{{item}}</li>
	</ul>

	<ul ng-sortable="{ group: 'foobar' }">
		<li ng-repeat="item in foo">{{item}}</li>
	</ul>

	<ul ng-sortable="barConfig">
		<li ng-repeat="item in bar">{{item}}</li>
	</ul>
</div>
```


```js
angular.module('myApp', ['ng-sortable'])
	.controller('demo', ['$scope', function ($scope) {
		$scope.items = ['item 1', 'item 2'];
		$scope.foo = ['foo 1', '..'];
		$scope.bar = ['bar 1', '..'];
		$scope.barConfig = {
			group: 'foobar',
			animation: 150,
			onSort: function (/** ngSortEvent */evt){
				// @see angular-legacy-sortable.js#L18-L24
			}
		};
	}]);
```

### Options

A hash of options can be provided to **[ng-sortable]** attribute. Available options are detailed in [SortableJS documentation](https://github.com/RubaXa/Sortable#options)

