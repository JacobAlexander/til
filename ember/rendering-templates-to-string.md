# Rendering templates to strings in Ember.js
Sometimes it can be useful to render the template of the component or route to string. As an example, you can think about situation when you need to have couple of predefined e-mail templates that has dynamic content and must be previewed on the app before sending.

They can be obtained by simple string interpolation, but it will eventually be really hard to maintain and improve. The solution is to make components that have templates with your predefined content and dynamic bindings. Afterwards you can render the component's template to string and show it in the app.

### Rendering template without any dependencies
Simple situation demands rendering template that does not have any dependencies such as other components or helpers. To do it you need `Ember.View` instance with mocked `Ember.Component` instance that holds your dynamic content.
```htmlbars
Hi! This is some template with dynamic content from {{content.name}}
```

```coffee
template = @container.lookup("template:some/path/to/template")
component = Ember.Component.create
  content: @get("someDynamicContent")
view = Ember.View.create
  template: template
  controller: component
view.createElement()
console.log(view.element.innerHTML)
```

### Rendering template with dependencies
If you need to use e.g. some helpers in your component, you need to use Ember injected method `createChildView`.
```htmlbars
Hi! This is some template with dynamic content from {{content.name}} and helper inside - {{formatted-date content.date}}
```

```coffee
template = @container.lookup("template:some/path/to/template")
component = Ember.Component.create
  content: @get("someDynamicContent")
view = @createChildView(Ember.View,
  template: template
  controller: component
)
view.createElement()
console.log(view.element.innerHTML)
```

### Furhter read
Very extensive explanation about why we need to use `createElement`, which is not defined particulary for that case, can be found [here](https://github.com/emberjs/ember.js/issues/5534#issuecomment-60527838). 
