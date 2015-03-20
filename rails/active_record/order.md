## Order

#### You should always use symbol notation syntax to avoid sql injection:

### BAD

``` ruby
class Controller
  def  action
    @ordered = ActiveRecordModel.order("column_name #{params[:order]}") # possible SQL injection
  end
end
```

### GOOD

``` ruby
class Controller
  def  action
    @ordered = ActiveRecordModel.order(column_name: params[:order]) # raise ArgumentError: Direction should be :asc or :desc
  end
end
```
