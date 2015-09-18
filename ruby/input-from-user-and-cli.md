So, you want a script that accepts both command line arguments and user input.

If you use simple `gets`, ruby will scream at you:


```ruby
  def initialize
    self.login = ARGV[0]
    print 'password: '
    self.password = gets.chomp
  end
  
  gets: No such file or directory @ rb_sysopen
```

`STDIN.gets` will work just as expected though!

```ruby
  def initialize
    self.login = ARGV[0]
    print 'password: '
    self.password = STDIN.gets.chomp
  end
  
  no errors whatsoever! \o/
```
