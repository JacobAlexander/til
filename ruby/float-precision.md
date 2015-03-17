## Float precision (format specifiers)

If you want to get a `Float` number converted to a `String` of a given precision, you can do:

```ruby
float = 123.45678
"%.4f" % float
# => "123.4568"

# or you can write it in a little bit different way

sprintf "%.4f", float
# => "123.4568"
```

Output value will be rounded automatically, so there is no need to call `round(x)` there.
This is especially useful when you want to have all the numbers of a given precision but some of them have zero (`0`) in the decimal part, so round won't be enough here:

```ruby
[0.0, 0.234, 0.7899].map { |n| n.round(3).to_s }
=> ["0.0", "0.234", "0.799"]

# but if you use format specifier:

[0.0, 0.234, 0.7899].map { |n| "%.3f" % n }
=> ["0.000", "0.234", "0.799"]

# you get what you need
```

## Further read

* [http://zetcode.com/lang/rubytutorial/strings/](http://zetcode.com/lang/rubytutorial/strings/) - very interesting and detailed read about *format specifiers*
