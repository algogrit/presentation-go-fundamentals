layout: true

.signature[@algogrit]

---

class: center, middle

# Go Fundamentals

Gaurav Agarwal

---
class: center, middle

Go is a compiled language. Every program needs to be compiled before it can be run!

---
class: center, middle

## Looking at `scratchpad.go`

---

## Running & Building

- `go build`

  > for compiling go program into a binary

- `go run`

  > for compiling and running the binary immediately

---

### Env variables

- `GOOS`

- `GOARCH`

[Possible values](https://gist.github.com/asukakenji/f15ba7e588ac42795f421b48b8aede63)

---
class: center, middle

## Naming conventions

---

- package names, directories, filenames

  > `snake_case`

- exported functions, variables, const, types

  > `PascalCase` / `UpperCamelCase`

- non-exported functions, variables, const, types

  > `lowerCamelCase`

---
class: center, middle

## Import & Exports

---

### Packages

- Every `.go` file starts with `package <name>`

- All `.go` files in a directory need to belong to the same package

- Every package needs to be in a directory of the same name

  - Except `main` package

- `func main` can only be defined in a `main` package

---

### Imports

Import path is always relative to `$GOPATH/src`

---
class: center, middle

> *unless you are using `go mod`*

---

### Exports

- Works using the first character -> uppercase means exported

### More info

```bash
go help importpath
```

---
class: center, middle

## Types

---
class: center, middle

Go is a statically typed, type inferred language!

---
class: center, middle

i.e.) You don't have to write a type of a variable explicitly, the compile will infer it. But all types must be known/inferred at compile time.

---

### Variables

- `var` keyword

#### Declaration & Initialization

- `var <name> <type>`

- `var <name> = <val>`

- `<name> := <val>`

---

## `builtin` types

```go
bool

string

int  int8  int16  int32  int64
uint uint8 uint16 uint32 uint64 uintptr

byte // alias for uint8

rune // alias for int32
     // represents a Unicode code point

float32 float64

complex64 complex128
```

---

- [Basic types](https://tour.golang.org/basics/11)

  - defined in the [`builtin`](https://golang.org/pkg/builtin/) package

- Know type information using `%T` [formatter](https://golang.org/pkg/fmt/)

- Type aliases using `type` keyword

---

## Default values

- zero values

---

- multiple assignment

```go
var i, j = "Hello", 42
```

---
class: center, middle

## Type conversion

---

- `<type>(<val-of-other-type>)`

  - Eg: `val := int(42.00)`

---

- Specialized type conversion
  - `strconv`

---
class: center, middle

## Constants

---

- `const` keyword

---

### Paired with `type` keyword, can be powerful

- `iota` built-in

---

#### `const` in the `time` package

- [`time.Weekday`](https://golang.org/pkg/time/#Weekday)

- [`time.Month`](https://golang.org/pkg/time/#Month)

- [`time.Duration`](https://golang.org/pkg/time/#Duration)

  - [Constants](https://golang.org/pkg/time/#pkg-constants)

---
class: center, middle

## Flow Control

---

### For

- normal `for <init>; <condition>; <post> {`

- while `for <condition> {`

- forever `for {`
  - can control execution using `break` & `continue`

---

### if

- with [statements](https://tour.golang.org/flowcontrol/6)

- `if <statement>; <condition> {`

  - `var`s declared within statement are available only within `if / else if / else` block

---

### [Switch statements](https://gobyexample.com/switch)

- no break

- statements are optional

- top-down execution - where execution stops after a case succeeds

- normal `switch <value> { case <match>`

- takes statement `switch <statement>; <value> { case <match>`

- conditional `switch { case <bool-statement>: `
  - `if-else-if`

---

### [Ranges](https://gobyexample.com/range)

- `for` along with `range`

  - range returns `index` & `element`

  - `for index, element := range "abc" {`

  - `for <index>, <value> := range <var> {`

- For maps *we will take a look at DS next*
  - `for <key>, <value> := range <map-type> {`

---
class: center, middle

## DS

---

### Arrays

- `var <name> [<length>]int`

- `len` & `cap` from `builtin`

- zero values?

---

*Go's declaration [syntax](https://blog.golang.org/declaration-syntax)*

---

### [Slices](https://blog.golang.org/slices-intro)

- `var <name> []int`

- References to underlying array

- `append`

  - Eg. `append(s, <element1>, <element2>, ...)`

  - You have to assign it back to `s` or whatever is your slice variable name

  - Can have a different behavior depending on capacity

- `make([]<type>, len, cap)`

- `make([]<type>, lenAndCap)`

---

- zero value of slices?

---

### Intro to structs

- Store related fields of different types

- `struct` keyword

  - Usage along with `type` keyword

  - Anonymous structs

- Struct Literal syntax

---

- zero value of structs?

---

### Maps

- `map` keyword
  - `map[<keyType>]<valType>`

- `make(map[string]Person)`

- `len` only

- `delete`
  - Eg. `delete(m, <key>)`

- lookup returns 2 values - `val, ok`

---

- zero value of maps?

---

- They need to be initialized before usage either with

  - `make`

  > `make(map[string]Person)`

  or

  - `map` literal syntax

  > `map[string]Person{}`

---

### Custom

- [generics](https://go.googlesource.com/proposal/+/refs/heads/master/design/go2draft-type-parameters.md) are coming in Go 2!

- Till then rely on `interface{}` or implement a DS for specific types

---
class: center, middle

Oops! We haven't talked about interfaces yet!

---
class: center, middle

> What happens to variables when we pass them to functions?

---
class: center, middle

## Pass by value

---

- Go is pass by value always!

- A few types have pointer fields under the hood
  - Eg.
    - `slices`
    - `maps`
    - `channels`

---
class: center, middle

## Pointers

---

- `p := &<variable>`

  - `var p *<type>`

- Print address using `%p` formatter

- `*` is used for dereferencing as well as defining a var as pointer

- `&` is used to get the address/reference of a variable

- `new` builtin function can initialize memory for any type

---

- No pointer arithmetic

  - You would have to use package [`unsafe`](https://golang.org/pkg/unsafe)

  *`unsafe` is beyond the scope of what we will cover*

- `unsafe` is used heavily internally

---
class: center, middle

## Functions

---

- Multiple Returns

- Named return values

- Variadic functions `...`

---
class: center, middle

### Functional Programming in Go

---

- Can be anonymous
  - `func (<argName> <type>) ({<rVarName>} <type>) {`

- First-class citizens
  - Can be passed around or assigned to variables

- closures
  - can capture variables from outer scope

---

- zero value of function variable?

---

class: center, middle

Code
https://github.com/algogrit/presentation-go-fundamentals

Slides
https://go-fundamentals.slides.algogrit.com
