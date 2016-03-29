## Using paperclip and CDN for serving images
### Problem
When you edit or reupload new version of an image with paperclip, without changing its filename, cloudfront will serve you the old version of this asset.

### Solution
To solve this problem, I added special method to every model which has an image attached. This method adds timestamp to attachment filename, every time it gets processed by paperclip.

```ruby
before_post_process :add_timestamp

def add_timestamp
  filename = File.basename((attachment.instance_read :file_name), '.*')
  ext = File.extname((attachment.instance_read :file_name))
  attachment.instance_write :file_name, "#{filename}#{Time.now.to_i}#{ext}"
end
```
