# Set

Set implements a collection of unordered values with no duplicates.
This is a hybrid of Array's intuitive inter-operation facilities and Hash's fast lookup.

The equality of each couple of elements is determined according to `Object#eql?` and `Object#hash`, since Set uses Hash as storage.

**Use case**

instead of:

```ruby
array = []
array << element unless array.include? element
```
you can use `Set`:

```ruby
set = Set.new
set << element
set << element # -> #<Set: {element}>
```

when order does matter let's try out `SortedSet`:

```ruby
sorted_set = SortedSet.new
sorted_set << element
```

## Further read

* [http://ruby-doc.org/stdlib-2.2.1/libdoc/set/rdoc/Set.html](http://ruby-doc.org/stdlib-2.2.1/libdoc/set/rdoc/Set.html)
* [http://ruby-doc.org/stdlib-2.2.1/libdoc/set/rdoc/SortedSet.html](http://ruby-doc.org/stdlib-2.2.1/libdoc/set/rdoc/SortedSet.html)
