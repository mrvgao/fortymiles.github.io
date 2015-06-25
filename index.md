# Angular Notes

1. Avoid minify

		function PhoneListCtrl($scope, $http){...}
		PhoneListCtrl.$inject = ['$scope', '$http'];
		phonecatApp.controller('PhoneListCtrl', PhoneListCtrl);
