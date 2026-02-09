## What is Carbun?
Carbun is a kind of low level compiled programming language made using python. it currently supports x86_64 linux. It is fully opensource. <br>

## Syntax
### Basics
Carbun has very simple syntax. the carbun file can have any extension. when compiling for OS level there must be a mandatory main subroutine like this: <br>
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

the `nl` command prints a newline. <br>

### Variables
There are 3 types of variables: quadword, bytes and arrays.<br>
To define a quadword you can use `var <varname>`. <br>
To define a byte you can use `byte <bytename>`. <br>
To define a var array you can use `var <name> [size]`. <br>
To define a byte array you can use `byte <name> [size]`. <br>

To set variable value you can use these: <br>
`setstr <var> "value"` : sets variable value to a string, max 8 bytes. <br>
`setint <var> 256` : sets variable value to an integer, max 8 bytes. <br>
`setchar <var> 255` : sets byte value to a byte, max 8 bit. <br>
`setvar <var> <var2>` : copies value of one variable to another. <br>
`setvar* <var> <var2>` : sets variable value to address if a variable. currently useless when using non-builtin functions. <br>
`setop <var> <val1> <op> <val2>` : sets variable value to value 1 operated by value 2. operations include +, -, / and *.

### Libraries
In carbun you can import libraries using the `#using` command, like: <br>
```
#using <ioutils.l>

sub main
  print_uint_w0 256
end sub
```
some libraries: <br>
`ioutils.l`: gives I/O helpers like `print_uint <val>`, `print_uint_w0 <val>`, `read_bytes_trim *<varname> <byte-to-trim>`, `print_int_array *<arrayname> <arraysize>`, `print_bytes_array *<arrayname> <arraysize>` and `print_byte_array *<arrayname> <arraysize>`. <br>
`byteutils.l`: gives functions for arrays like `push_bytes *<array-name> <index> <byte>` and others. <br>
`bareutils.l`: gives VGA Write function, still under testing. <br>
`mathutils.l`: gives functions like `sqr <value> *<result-var>`, `cube <value> *<result-var>` and `mean *<result-name> *<array-name> <num-of-observations>`. <br>

### If condition
If conditions use the `if` command in carbun. you can use them like this:
```
#using <ioutils.l>

var inp
sub main
  read_bytes_trim *inp 10
  if inp == "Hello"
    echo bytes "Hello"
  end if
end sub
```

### While loops
While loops are defined using `while` command. with syntax `while <val1> <op> <val2>...end while`. example: <br>
```
#using <ioutils.l>

var x

sub main
  while x != "exit"
    echo bytes "> "
    read_bytes_trim *x 10
  end while
end sub
```

### Assembly in carbun???
Yes. you read that right, in carbun you can use the `asm` command to run assembly, like `asm xor rax, rax`. <br>

### Subroutines
to define a subroutine you can use `sub <name>...end sub` syntax. like: <br>
```
sub mysub
  asm nop
end sub
```
to exit a subroutine midway you can use `end sub`, to exit while returning a value you can use `return <val>`, and you can use `lastret <var>` to store that value to a variable. example: <br>
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

# Fix reports
v1.1lerbb: Fixed array memorey leak. <br>
v1.2lerbb: Fixed byteutils.l. <br>
v1,3lerab: Made byte arrays. fixed a few functions. removed `check_bytes` from `byteutils.l`. made a highlighter extension for VSCode

# Install and Setup
### Debian/Ubuntu
You can download the .deb given here and use `sudo apt` to install. after wards do `sudo mklib` to initialize the libraries. they after writing a script you can do `carbun <infile>.cb <output>` and then do `./<output>`
