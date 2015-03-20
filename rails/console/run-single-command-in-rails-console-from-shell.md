# Run single command in Rails console from shell

With plain Ruby we can obviously use the *eval* option:

```ruby
> ruby -e "print 'hello'"
hello
```

But `rails console` can't do that. Lucky for us, we can just
pipe things to the command, the old unix way:

```ruby
> echo "User.first.name" | rails c
# ...
=> "John"
```

And then we can pipe results further to the grep or
[ag](https://github.com/ggreer/the_silver_searcher) for example. It's
nothing new but it's easy to forget how flexible tools we
have at our fingertips.
