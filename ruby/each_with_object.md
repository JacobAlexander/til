# Using inject for creating hashes

Let's say I want to create a hash of the following structure:

```ruby
{
  'foo' => random_number,
  'bar' => random_number,
  'baz' => random_number
}
```

Using an array of keys and inject:

```ruby
fields = %w(foo bar baz)
fields.inject({}) do |memo, field|
  memo[field] = rand(1000)
  memo
end
```

When I was checking my code with rubocop before commiting, I've seen the following message - `Use each_with_object instead of reduce`. So after a quick google search:

```ruby
fields = %w(foo bar baz)
fields.each_with_object({}) do |field, memo|
  memo[field] = rand(1000)
end
```

`each_with_object` unconditionally passes the object with which it was initialized, so you don't have to explicitly return it from the block.

Further reading:
http://www.bbs-software.com/blog/2013/11/22/rubys-injectreduce-and-each_with_object/
