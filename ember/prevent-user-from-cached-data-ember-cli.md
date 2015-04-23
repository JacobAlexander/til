# Prevent user from getting cached data after e.g. another user

Let's say we have an authentication system (like [ember-simple-auth](https://github.com/simplabs/ember-simple-auth)). Even though, that it's not most common case, it may happen that one user will log out and another one will log in using same browser window. There are some issues that may happen strange behaviours due to `DS.Store` automatic caching mechanism.

### Example
Let's say that on some route, called `posts` we get all posts from backend API. On backend, we check the current user and decide which posts to return.

```coffee
# app/routes/posts.coffee
model: ->
  @store.find("post")
```

Even after log out using some kind of invalidating session (in ember-simple-auth it is called `#invalidateSession`) the results will be cached into `DS.Store` instance. This means, that after the second user signs into the app, on the same route he will get his results AND the results cached from former user.

The reason is that `DS.Store` has no knowledge that these requests may be different as we do not provide any sign that it depends on the signed in user.

### Solution
The simplest way to clear cache stored by `ember` and `ember data` is to call [`Ember.Application#reset()`](http://emberjs.com/api/classes/Ember.Application.html#method_reset). However, developers can also store state of the app in globals, that are holding e.g. other JavaScript libraries. To make sure that after signing out, the next user will get clean app is to reload the page:
```coffee
@get("session").invalidate()
window.location.reload()
```

### Further read
* [`Ember.Application#reset()`](http://emberjs.com/api/classes/Ember.Application.html#method_reset)
* [Automatic caching in `ember data`](http://guides.emberjs.com/v1.11.0/models/#toc_automatic-caching)
* [Nice post on Ember Discuss](http://discuss.emberjs.com/t/calling-app-reset-in-ember-cli-project/6351)
