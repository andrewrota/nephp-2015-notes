**Advanced Debugging Techniques for PHP** by [Patrick Allaert](https://twitter.com/patrick_allaert)

http://slides.catchy.io/Advanced-debugging-techniques-for-PHP.html

**Debugging What?**

* XDebug
* PHPdbg
* phptrace
* strace
* ltrace
* inotify

#### PHP Debugging

 **PHPdbg**

Native debugger.

 `break 3` to add break point at ln3, then run `run`.  Use `step` command to advance to next line.  `continue` to next breakpoint.  `ev $hello` to evaluate var `$hello`.

**phptrace**

Low overhead tracking tool composed of a PHP extension and a CLI.

`-s` will give status at a particular point

#### System Debugging

**strace**

Trace any system calls done by a program.

`strace -e file ls`

**ltrace**

Trace any library calls done by a program.  Not just between process and system globally.  This can be very verbose.