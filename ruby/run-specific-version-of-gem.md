# Run specific version of a gem

**Question:** if I have multiple versions of Rails installed (assuming I am lazy and have only one gemset) - how do I run a specific version e.g. create new Rails project in _4.0.9_ and not _4.2.1_?

**Answer:** just use `<gem_name> _<gem_version>_ [options]` pattern.

```shell
❯ rails --version
Rails 4.2.1

❯ rails _4.0.9_ --version
Rails 4.0.9
```
