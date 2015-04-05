# Specify compiler to use for bundle install

**Case:** I wanted to install the [beybug](https://github.com/deivid-rodriguez/byebug) gem. So I've tried:

```shell
❯ gem install beybug -v '4.0.5'
```

It gave me error (failed to compile)  with something significant in the middle:

```shell
compiling breakpoint.c
error: unknown warning option '-Wno-packed-bitfield-compat'; did you mean '-Wno-keyword-compat'? [-Werror,-Wunknown-warning-option]
```

Google said that GCC 4.4 or lower doesn't know how to handle this command. But what the heck, is my OS X packing such an old version of GCC? Nope.

```shell
❯ gcc -v
Configured with: --prefix=/Applications/Xcode.app/Contents/Developer/usr --with-gxx-include-dir=/usr/include/c++/4.2.1
Apple LLVM version 6.0 (clang-600.0.57) (based on LLVM 3.5svn)
Target: x86_64-apple-darwin14.1.0
Thread model: posix
```

It's **Clang**.

XCode is overriding my GCC of choice installed by the brew command. Now that's not cool. I could override this or use a symlink (lol, nope, I'm so lazy!) - but this would mean messing with XCode and I need it to also work.

Solution? As old as the hills. Override the env variable responsible for telling _makefiles_ which compiler they should use. And that's a `CC` env:

```
❯ CC=/usr/local/Cellar/gcc/4.9.2_1/bin/gcc-4.9 gem install byebug -v '4.0.5'
Building native extensions.  This could take a while...
Successfully installed byebug-4.0.5
1 gem installed
```
