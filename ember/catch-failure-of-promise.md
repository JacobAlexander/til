# Catching failure of promise

Most of ember-data methods return promises. We have two ways of handling success and failure of the promise [according to Ember Guides](http://emberjs.com/api/classes/RSVP.Promise.html):
* using [RSVP.Promise#then](http://emberjs.com/api/classes/RSVP.Promise.html#method_then) and it's two callbacks - one for success and one for failure
* using [RSVP.Promise#catch](http://emberjs.com/api/classes/RSVP.Promise.html#method_catch)

However, there is a major difference between these two! The `then` failure callback will fire only in case of failure response from Promise (e.g. from API). `catch` method will fire both in case of failure response **and** in case of exception in `then`'s callback code.

```coffeescript
@store.find('someModel').then( (records) ->
  # do sth but accidentally raise exception (e.g. by calling `undefined`)
).catch (reason) ->
  # this code will execute everytime due to fact of exception in `then`, 
  # even if response from `find` is success!
```
Above example will silently fail due to fact of exception and can be mistaken as response failure.

To sum up, it is more safe to use as follows:
```coffeescript
@store.find('someModel').then ((records) ->
  # do sth
), (reason) ->
  # this code will execute only in case of failure in response
  # if exception happens in `success`, it will be printed out to console as usual
```
