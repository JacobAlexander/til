# Debugging with pry

We all know that when it comes to Ruby/Rails debugging - Pry is our choice.
Here's a list of a few useful things:

* showing source of the method by using `$ your_method`:

	```ruby
	> repo = UserRepository.new
	#=> #<UserRepository:0x007fdc22a0f6f8>
	> $ repo.all_by_name

	From: app/repositories/user_repository.rb @ line 23:
	Owner: UserRepository
	Visibility: public
	Number of lines: 3

	def all_by_name
	  User.by_name
	end
	```
	
* `cd` into method:

	```ruby
	> cd repo
	#=> pry(#<UserRepository>):1> 
	> self.class
	#=> UserRepository < Object
	```
* `ls` - list methods in current scope:
	
	```ruby
	> pry(#<UserRepository>):1> ls
	#=> UserRepository#methods: active  all_by_name  from_api  get  items
	#=> self.methods: __pry__
	#=> locals: _  __  _dir_  _ex_  _file_  _in_  _out_  _pry_
	```

## Further read

* [RailsConf 2014 - Debugger Driven Developement with Pry by Joel Turnbull
](https://www.youtube.com/watch?v=4hfMUP5iTq8)
* [pry/pry](https://github.com/pry/pry)
* [plugin set for rails](https://github.com/netguru/jazz_hands): syntax highlighting as you type, stack exlorer, etc.