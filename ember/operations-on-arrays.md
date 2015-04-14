# Operations on arrays

If you want to manipulate plain `Array` object in Ember you should use methods provided by `Ember.Array` class. They are integrated in Ember run loop and does not break seamless bindings between templates and observers.

### BAD

```coffeescript
@get("someArray").push(newObject)
```

It will not seamlessly update binding with following template:
```handlebars
{{#each item in someArray}}
  <p>{{item}}</p>
{{/each}}
```

### GOOD

```coffeescript
@get("someArray").pushObject(newObject)
```

It will update the templates and trigger the observers to execute.

Other examples of differences between plain `Array` and `Ember.Array` are below:
* `push` vs `pushObject`
* `pop` vs `popObject`
* `unshift` vs `unshiftObject`

Best way to make sure that your arrays are always correctly managed is to use `Ember.Array` instead of plain `Array` object. However, default Ember behavior enebles prototype extensions and extend `Array` object to support all behavior from `Ember.Array`, `Ember.Enumerable`, `Ember.MutableEnumerable` and `Ember.MutableArray`.

More information about `Ember.Array` class is [here](http://emberjs.com/api/classes/Ember.Array.html).
