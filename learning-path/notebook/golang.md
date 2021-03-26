# Golang

## Go vs pyton, c/c++, java

- python is easy but slow;
- java has complex type system, so as c/c++;
- c/c++ also slow compile;
- Go is highly parallel highly concurrency:
  - strong and statically typed as c/c++ or java, but the compiler will done it for you;
  - exallent community;
  - key features:
    - simplicity;
    - fast compile time;
    - garbage collected;
    - built-in concurrency;
    - compile to standalone binaries;


## Go Resources

- <https://golang.org>

## Install

```zsh
# check go path is right
go version

# set path to store packages
export GOPATH=~/golib
export PATH=PATH:GOPATH/bin
export GOPATH:=$GOPATH:~/gocode  # compond gopath, when downloading, first path is used, but both dirs could be read

# try install a package path
go get github.com/mdempsky/gocode
# cd ~/golib/ to check if there is the package

# create bin, src, pkg for gocode dir
cd ~/gocode
mkdir bin src pkg

# other packages location in macOS
cd /usr/local/Cellar/go/1.15.6/libexec
```

## Start Code

- install language tools: <https://github.com/golang/tools/blob/master/gopls/doc>
- then:
```zsh
# go can read from your github, so just create project like github
cd ~/gocode

mkdir -p /src/github.com/sheldonldev/gohello

touch /src/github.com/sheldonldev/gohello/Main.go
vim /src/github.com/sheldonldev/gohello/Main.go
```

```go
package main

import "fmt"

func main() {
  fmt.Println("Hell, Golang!")
}
```

```zsh
go run src/github.com/sheldonldev/gohello/Main  # 运行
go build github.com/sheldonldev/gohello         # 二进制
./gohello                                       # 运行二进制
go install github.com/sheldonldev/gohello       # 安装二进制到 $GOPATH/bin
bin/gohello                                     # 运行已安装的二进制
```

## Variables

### Variable Declaration

- Ways to declaration

```go
// 1. 
var i int  // 0 is the default when init
i = 42
i = 27

// 2.
var i int = 42

// 3.
i := 42   // will be error if it's the redeclaration

// === play
var i int
i = 42
var j float32 = 27
k := 99.
fmt.Printf("%v, %T\n", i, i)
fmt.Printf("%v, %T\n", j, j)
fmt.Printf("%v, %T\n", k, k)

// 4.
var (
  actorName string = "Elisabeth Sladen"
  doctorNumber int = 3
)
```

### Redeclaration and Shadowing

```go
var i int = 27
func main() {
  // i := 42      // this way of redeclaration is not allowed
  var i int = 42  // this way will be fine, it's called shadowing
  // j := 17      // in this way, declared but not used, is not allowed
  fmt.Println(i)  // 42
}
```

### Visibility

- Package Level vs. Block Scope
- Package level variables lowercase first;
- To export globally, uppercase first;

### Naming Conventions

- Pascal or camelCase;
- Capitalize acronyms;
- Examples to keep code cleaner: theHTTP, theURL, theHttpRequest;
- As short as reasonable, longer names for longer lives;

### Type Conversions

```go
var i float32 = 42.5

// 1.
var j int
j = int(i)  // explicit convertion is a must

// 2.
var j string
j = string(i)
fmt.Printf("%v, %T", j, j) // need transform coding, see following
// *, string

import (
  //...
  "strconv"
)
var j string
j = strconv.Itoa(i)
fmt.Printf("%v, %T")
```

## Primitives

### Boolean

```go
// 1.
var n bool = false

// 2.
n := 1 == 1 // true
m := 1 == 2 // false

// 3.
var n bool  // any undeclared is 0, and 0 is false
```
### Numeric

#### Integers

- signed:
  - int8: -128 ~ 127;
  - int16: -32,768 ~ 32,767;
  - int32;
  - int64;
- unsigned:
  - uint8: 0 ~ 255;
  - uint16: 0 ~ 65,535;
  - uint32;
  - uint64;

```go
a := 10
b := 3
// all results are integers
fmt.Printf("%v, %T\n", a + b, a + b)
fmt.Printf("%v, %T\n", a - b, a - b)
fmt.Printf("%v, %T\n", a * b, a * b)
fmt.Printf("%v, %T\n", a / b, a / b)
fmt.Printf("%v, %T\n", a % b, a % b)

// must the same type
a := 10
var b int8 = 3
// fmt.Printf("%v, %T\n", a + b, a + b) // error
fmt.Printf("%v, %T\n", a + int(b), a + int(b))

// binary operation
a := 10 // 1010
b := 3  // 0011
fmt.Println(a & b)  // and, 0010, 2
fmt.Println(a | b)  // or,  1011, 11
fmt.Println(a ^ b)  // exclusive, 1001, 9
fmt.Println(a &^ b) // andor,     0100, 8

// bit shift
a := 8  // 100, 2^3
fmt.Println(a << 3) // 100 000, 2^3 * 2^3, 64 
fmt.Println(a >> 3) // 1      , 2^3 / 2^3, 1
```

#### Floating Point

- float32, +- 1.18 e -38  ~ +- 1.18 e +38 ;
- float64, +- 2.23 e -308 ~ +- 2.23 e +308;

```go
var n float32 = 3.14
// n = 7.2e72 // overflow error
n = 2.1E14
fmt.Printf("%v, %T", n, n)

//
n := 3.14   // float64
n = 7.2e72  // no overflow error
n = 2.1E14
fmt.Printf("%v, %T", n, n)

//
a := 10.2
b := 3.7
// all are float64
fmt.Printf("%v, %T\n", a + b, a + b)
fmt.Printf("%v, %T\n", a - b, a - b)
fmt.Printf("%v, %T\n", a * b, a * b)
fmt.Printf("%v, %T\n", a / b, a / b)
// fmt.Printf("%v, %T\n", a % b, a % b) // not defined error
```

#### Complex Numbers

- Powerful for data science;
- complex64 and complex128;

```go
var n complex64 = 1 + 2i
fmt.Printf("%v, %T\n", n, n)

a := 1 + 2i
b := 2 + 5.2i
// all in complex128
fmt.Printf("%v, %T\n", a + b, a + b)
fmt.Printf("%v, %T\n", a - b, a - b)
fmt.Printf("%v, %T\n", a * b, a * b)
fmt.Printf("%v, %T\n", a / b, a / b)

//
var n complex64 = 1 + 2i
fmt.Printf("%v, %T\n", real(n), real(n)) // 1, float32, real part
fmt.Printf("%v, %T\n", imag(n), imag(n)) // 2, float32, imaginary part

//
var n complex128 = 1 + 2i
fmt.Printf("%v, %T\n", real(n), real(n)) // 1, float64
fmt.Printf("%v, %T\n", imag(n), imag(n)) // 2, float64

//
var n complex128 = complex(1, 2)
fmt.Printf("%v, %T\n", n, n)
```

### Text

#### String

- UTF-8

```go
s := "this is string"
// s[2] = "u" // immutable error
s1 := "string 1"
s2 := "string 2"
fmt.Printf("%v, %T\n", s, s)
fmt.Printf("%v, %T\n", s[2], s[2]) // 105, unit8
fmt.Printf("%v, %T\n", string(s[2]), s[2]) // i, unit8
fmt.Println(s1 + " " + s2)

// convert to collection of bytes
s := "this is string"
b := []byte(s) // a colection of unit8

```

#### Char

- UTF-32/unit32

```go
r := 'a'
// or
var r rune = 'a'

fmt.Printf("%v, %T\n", r, r) // i, unit32
```

## Constants

### Naming Convention

```go
const myConst = "" // package level
const MyConst = "" // for export
```
### Typed Constants

```go
const myConst int = 12
// myConst = 60  // error

//
// const myConst float64 = math.Sin(1.57)  // error, must can be determined at the first time

//
const myConst int16 = 27
func main() {
  const myConst int = 14  // inner shadowing is allowed
}

//
const myConst int = 14
var b int = 3
b + myConst // int

const myConst int = 14
var b int16 = 3
b + myConst // error
```

### Untyped Constants

```go
const myConst = 14
var b int16 = 3
b + myConst // int16, the same as: b + int16(42)
```

### Enumerated Constants

```go
const (
  a = iota  // iota is for enumerating, start from 0 as default
  b = iota  // iota increased by 1
  c = iota  // 3
)
func main() {
  fmt.Println(a)
  fmt.Println(b)
  fmt.Println(c)
}

// same as above, go will follow the pattern
const (
  a = iota
  b
  c
)

// two parallel iotas
const (
  a = iota
  b
  c
)
const (
  a2 = iota
  b2
  c2
)
func main() {
  fmt.Println(a)
  fmt.Println(b)
  fmt.Println(c)
  fmt.Println(a2)
  fmt.Println(b2)
  fmt.Println(c2)
}
```

### Enumeration Expressions

```go
// application 1.
const (
  _ = iota  // ignore first value
  KB = 1 << (10 * iota)
  MB
  GB
  TB
)
func main() {
  fileSize := 400000000000.
  fmt.Println(KB)
  fmt.Println(MB)
  fmt.Println(GB)
  fmt.Printf("%.2f GB", fileSize/GB)
}

// application 2.
const (
  isAdmin = 1 << iota
  isHeadquaters
  isFinancials
  isAsian
  isAfrican
  isEurapian
  isAustralian
  isAmerian
)
func main() {
  var roles byte = isAdmin | isHeadquaters | isAmerian
  fmt.Printf("%b\n", roles)
  fmt.Printf("%v\n", roles & isAdmin == isAdmin)        // true 
  fmt.Printf("%v\n", roles & isEurapian == isEurapian)  // false
}
```
