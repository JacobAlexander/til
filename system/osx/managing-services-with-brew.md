# Managing services with brew

If you want to have a nice way of starting/stopping services managed by
`homebrew`, and don't want to use `launchctl` interface, you might want to
check `brew services`.

It looks like this:

```
❯ brew services list
rabbitmq   started      476 /Users/adamo/Library/LaunchAgents/homebrew.mxcl.rabbitmq.plist
mongodb    started     3606 /Users/adamo/Library/LaunchAgents/homebrew.mxcl.mongodb.plist
postgresql started      485 /Users/adamo/Library/LaunchAgents/homebrew.mxcl.postgresql.plist
redis      started      471 /Users/adamo/Library/LaunchAgents/homebrew.mxcl.redis.plist
```

You can use commands like `list`, `restart`, `start`.

## Installation

```shell
brew tap gapple/services
```

## Usage

```
brew start mongodb
brew stop redis
brew restart postgresql
```

## Additional info

* [blogpost entry](https://robots.thoughtbot.com/starting-and-stopping-background-services-with-homebrew)
