# Acceptance testing of ember-select-2 component

In couple of our projects we use [ember-select-2](https://github.com/iStefo/ember-select-2) addon. It wraps Select2 component into ember-cli addon.

Unfortunately, it oftern turns out to be quite demanding task to write acceptance tests for that component. Below are few snippets that do their job (but remember to use `andThen` after them!):

### Open the dropdown
`click(".select2-choice")`

### Find search input
`$(".select2-search:last input")`

### Enter some query
```
input = $(".select2-search:last input")
triggerEvent(input, 'keydown')
fillIn(input, "Some query")
triggerEvent(input, 'keyup')
```

### Find the results
`$(".select2-result-selectable")`

### Find no results
`$(".select2-no-results")`

### Chose the results
`click($(".select2-result-selectable"))`

All of the above are proper only for single select2 and single result. But it's not a challange to chose from multiple results.

Please notice that we use `Ember.$` as finder of DOM elements, as `ember-select-2` is adding a layer into `<body>` element, which in case of tests is a wrapper for test suite, not an application itself. That's why ember helpers (e.g. `find`) cannot find these elements. The only part that works is to find and click select2 dropdown.
