Angular.bind is a utility function that combines functionality in function.bind and partial function application.

Binding (in general) is the idea that you want to bind the current context to a function, but actually execute it at a later time.

This can be useful in angular when making HTTP calls with $http and handling promises:

$http.get('url').then(angular.bind(this,
    function(response) {
        this.response = response; //use this (which is the bound context)
    });

In the above example, the this inside the function would not refer to the this in the $http context unless we explicitly bind it. This is a common JavaScript issue (in callbacks) because of its dynamic binding of context (which is unlike most popular class-oriented languages).

Partial Application is used when you want to make a function that has already been passed some of its arguments. A very simple example:

function add(x, y) {
    return x + y;
}

var add10To = angular.bind(this, add, 10);

console.log(add10To(5));
// outputs 15
