## Frozen scopes and constants 

#### There is a reason for the scope to be always in lambda:

### BAD, possible in rails 3.x not possible in 4.x (yields error) 

``` ruby
class Model
  scope :latest, where(["created_at > ?", 3.days.ago]) 
end
```

This is bad because it's evaluated only once when the class is loaded. So if you restart your server on Wednesday this `3.days.ago` will always be monday. 
What's even worse is the fact that it will work on development - on dev classes are reloaded on every request. Same for tests.  

### GOOD

``` ruby
class Controller
  scope :latest, -> { where(["created_at > ?", 3.days.ago]) } 
end
```
This is good becouse the lambda will always be evaludated when the scope is called. No more stubbed values.

It's important to remeber this will also happen when you use constants:

### BAD, possible in ruby all the time 

``` ruby
class Model
  LATEST_PERIOD = 3.days.ago 
  scope :latest, -> { where(["created_at > ?", LATEST_PERIOD]) } 
end
```

Lambda does not help here because the date was loaded into constant, and again, on production, that happens only when the server is started. So it's really 3.days.ago from the last server restart.

You can fix this by introducing class method i.e.: 
### GOOD

``` ruby
class Controller
  def self.latest_period
    3.days.ago 
  end 
  scope :latest, -> { where(["created_at > ?", latest_period]) } 
end
```
