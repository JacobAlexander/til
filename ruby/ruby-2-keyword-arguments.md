Ruby 2.1 has support for keyword arguments.



```ruby
def do_something(arg1:, arg2:)
```

It's easy to specify default values:

```ruby
def do_something(arg1: 1, arg2: 'a')
```

This is awesome for many reasons!

- You can pass arguments in any order to the method: `do_something(arg2: '', arg1: '')`.
- You can set default values on any of the arguments. (In the past the default values were last)
- It makes the arguments much easier to read when looking at method calls at a glance, especially when there are more than 2 arguments.
- It saves all the boilerplate of merging an options hash in methods!!

[More on thoughtbot](https://robots.thoughtbot.com/ruby-2-keyword-arguments)
