# Run specific version of a gem

Question: if I have multiple versions of Rails installed (assuming I am lazy and have only one gemset) - how do I run a specific version e.g. create new Rails project in 4.0.9 and not 4.2.1?

Answer: just use `<gem_name> _<gem_version> [options]` pattern.

```shell
❯ rails --version
Rails 4.2.1

❯ rails _4.0.9_ --version
Rails 4.0.9
```
