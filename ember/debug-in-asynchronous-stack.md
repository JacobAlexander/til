# Debug in asynchronous stack
Ember is very asynchronous framework where very often code is executed in some kinds of callbacks (promises, `Ember.run` and others). Any exceptions that will occur in that callbacks will be shown in console but the stack will not provide any information where the exception happen.

To enable asynchronous stack we need to check this option in Google Chrome Developer Tools -> Tab `Sources`. On right panel we will see tab `Call Stack` and the option `Async` to check.

### Further read
[Nice blogpost about async debugging](http://www.html5rocks.com/en/tutorials/developertools/async-call-stack/)
