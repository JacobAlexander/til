So, you want a script that accepts both command line arguments and user input.

If you use simple `gets`, ruby will scream at you:
`gets': No such file or directory @ rb_sysopen

`STDIN.gets` will work just as expected though!
