## What is Carbun?
Carbun is a kind of low level compiled programming langauge made using python. it currently supports x86_64 linux. It is fully opensource. <br>

## Syntax
### Basics
Carbun has very simple syntax. the carbun file can have anyy extension. when compiling for OS level there must be a mandatory main subroutine like this: <br>
```
sub main
  asm nop
end sub
```

### I/O
To print a string you can use `echo bytes <bytes>` like: <br>
```
sub main
  echo bytes "Hello world!"
end sub
```

To print an integer you can use `echo int <value>` like: <br>
```
sub main
  echo int 256
end sub
```

To read a string you can use `listen bytes <variable>` like: <br>
```
var x

sub main
  listen bytes x
  echo bytes x
end sub
```

To read an integer you can use `listen int <variable>` like: <br>
```
var x

sub main
  listen int x
  echo int x
end sub
```

the `nl` command prints a newline.

### Variables
There are 3 types of variables: quadword, bytes and arrays.<br>
to define a quadword you can use `var <varname>`. <br>
to define a byte you can use `byte <bytename>`. <br>
to define an array you can use `var <name> [size]`. <br>

### Libraries
In carbun you can import libraries using the `#using` command, like: <br>
```
#using <ioutils.l>

sub main
  print_uint_w0 256
end sub
```
some libraries: <br>
`ioutils.l`: gives I/O helpers like `print_uint <val>`, `print_uint_w0 <val>` and `read_bytes_trim *<varname> <byte-to-trim>`.
`byteutils.l`: gives functions for arrays like `push *<array-name> <index> <byte>` and others.
`bareutils.l`: gives VGA Write function, still under testing.
`mathutils.l`: gives functions like `sqr *<result-var> <value>`, `cube *<result-var> <value>` and `mean *<result-name> *<array-name> <num-of-observations>`

### If condition
If conditions use the `if` command in carbun. you can use them like this:
```
#using <ioutils.l>

var inp
sub main
  read_bytes_trim inp 10
  if inp == "Hello"
    echo bytes "Hello"
  end if
end sub
```

### Subroutines
to define a subroutine you can use `sub <name>...end sub` syntax. like: <br>
```
sub mysub
  asm nop
end sub
```
to exit a subroutine mid way you can us `end sub`, to exit while returning a vlue you can use `return <val>`, and you can use `lastret <var>` to store that value to a variable. example: <br>
```
sub test
  return "hi"
end sub

var x

sub main
  test
  lastret x
  echo bytes x
  nl
end sub
```

### Bugs and warnings report.
- `echo int` cannot print if value = 0. use `print_uint_w0` from ioutils.l for that instead.
- `listen bytes` returns byte 10 (newline) with the result
- `echo bytes` and `listen bytes` can take up space in final result due to them being inlines.
