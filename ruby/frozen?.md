In ruby 2.2.0 `#frozen?` method is changed for `true`, `false`, `nil` values.


### Ruby <= 2.1.7
```
[1] pry(main)> true.frozen?
=> false
[2] pry(main)> nil.frozen?
=> false
[3] pry(main)> false.frozen?
=> false
```

### Ruby >= 2.2.0
```
[1] pry(main)> true.frozen?
=> true
[2] pry(main)> false.frozen?
=> true
[3] pry(main)> false.frozen?
=> true
```

Moar reading:
https://bugs.ruby-lang.org/issues/8923
