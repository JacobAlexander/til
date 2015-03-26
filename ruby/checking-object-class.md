# Checking object class

Often you have to check if the object you're dealing with is of a proper type.
Here's some examples you might find useful:

Let's have two basic classes:

```ruby
class Foo
end

class Bar < Foo
end
```

Of course we can compare classes like this:

```ruby
#> foo = Foo.new
#> foo.class == Foo
#> true
```

but there is much nicer way - using `is_a?` / `kind_of?`:

```ruby
#> bar = Bar.new
#> bar.is_a?(Bar)
#=> true
#> bar.kind_of?(Foo)
#=> true
```

If you have to check if some class inherits after another one, there is also a nice way to do that:

```
#> Bar < Foo
#=> true

#> Foo > Bar
#=> true
```

## Further read

* [Object class in Ruby](http://ruby-doc.org/core-2.2.1/Object.html#method-i-is_a-3F)
* [more about object equality](http://taylor.fausak.me/2014/05/24/class-comparison-in-ruby/)
