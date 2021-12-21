# Golang
## Variables
### Basic Types
* Integers
  + Signed
    - int
    - int8
    - int16
    - int32
    - int64
  + Unsigned
    - uint
    - uint8
    - uint16
    - uint32
    - uint64
* Floats
  + float32
  + float64
* Complex Numbers
  + complex64
  + complex128
* Byte - alias for uint8
* Rune - alias for int32 (unicode code point)
* String
* Boolean

Sizes as in C ++
### Variable Declaration
```go
var i int
```
```go
var i int = 32
```
```go
var i = 32
```
```go
i := 32
```
```go
var (
  i int
  j int
)
```
**You can't redeclare variables, but you can shadow them**
```go
func main() {
  var i int = 100
  i := 50
}
```
_Output - CE_
```go
package main

import "fmt"

var i = 200

func main() {
	i := 30
	fmt.Print(i)
}
```
_Output - 30_

**All variables must be used**
```go
package main

func main() {
	i := 30
}
```
_Output - CE_

**All unitialized variables have a zero value**
```go
package main

import "fmt"

func main() {
	var n bool
	var i int
	var j float32
	var k complex64
	fmt.Print(n, i, j, k)
}
```
_Output - false 0 0 (0+0i) 0_

**You can only apply math operations to the same types**
```go
func main() {
	a := 10
	b := 12
	c := b - a
	fmt.Printf("%v %T\n%v %T\n%v %T", a, a, b, b, c, c)
}
```
_Output - 10 int 12 int 2 int_

```go
func main() {
	var a uint8 = 10
	b := 12
	c := b - a
	fmt.Printf("%v %T\n%v %T\n%v %T", a, a, b, b, c, c)
}
```
_Output - CE_

**Exponential notation**
```go
package main

import "fmt"

func main() {
	a := 13.4e10
	b := 13.4E10
	fmt.Print(a, b, a == b)
}
```
_Output - 1.34e+11 1.34e+11 true_

**Strings are immutable**
```go
package main

import "fmt"

func main() {
	s := "this is a string"
	s[2] = 's'
}
```
_Output - CE_

**String vs []rune()**

String value is a read-only byte slice. And, a string literal is encoded in utf-8. Each char in string actually takes 1 ~ 3 bytes, while each rune takes 4 bytes.
```go
package main

import "fmt"

func main() {
	s := "this is a string"
	r := []rune("this is a string")
	r[0] = 'T'
	fmt.Printf("%v %T %v\n%v %T %v", s, s, len(s), string(r), r, len(r))
}
```
Output -

this is a string string 16

This is a string []int32 16
	 
### Bitwise operations
```go
package main

import "fmt"

func main() {
	var a uint8 = 10 // 00001010
	var b uint8 = 12 // 00001100
	fmt.Println(^a) // not a = 11110101 = 245
	fmt.Println(a & b) // a and b = 00001000 = 8
	fmt.Println(a | b) // a or b = 00001110 = 14
	fmt.Println(a ^ b) // a xor b = 00000110 = 6
	fmt.Println(a &^ b) // a and not b = 00001010 & 11110011 = 00000010 = 2
	fmt.Println(a |^ b) // a or not b =  00001010 | 11110011 = 11111011 = 251
	fmt.Println(a ^^ b) // a xor not b = 00001010 ^ 11110011 = 11111001 = 249
	fmt.Println(a ^^^ b) // a xor (^^ b) = a xor (not not b) = a xor b = 6
	fmt.Println(a << 3) // a << 3 = 00001010 << 3 = 00001010 = 80
	fmt.Println(b >> 5) // b >> 5 = 00001100 >> 5 = 00000000 = 0
}
```
### Const key-word
```go
func main() {
	const myConst uint = 13
	fmt.Printf("%v %T", myConst, myConst)
}
```
_Output - 13 uint_

**Const values has to be assigned at compile time**
```go
func main() {
	const myConst = math.Exp(1.23)
	fmt.Printf("%v %T", myConst, myConst)
}
```
_Output - CE_

**Arrays are always going to be variable**
```go
func main() {
	s := "some string"
	const myConst = []byte(s)
	fmt.Printf("%v %T", myConst, myConst)
}
```
_Output - CE_

**Compiler is basically replacing every instance**
```go
func main() {
	const a = 123 + 4
	var b float64 = 12.7
	fmt.Println(math.Ceil(a * b))
}
```
_Output - 1613_

**Enumerated consts**
**Iota scoped to a constant block**
```go
const (
	a = iota
	b
	c
)

const (
	d = iota
)

func main() {
	const (
		e = iota
	)
	fmt.Println(a, b, c, d, e)
}
```
_Output - 0 1 2 0 0_

```go
const (
	_ = iota + 12
	a
	b
	c
)


func main() {
	fmt.Println(a, b, c)
}
```
_Output - 13 14 15_

```go
const (
	_ = iota + 12
	a
	b = iota + 3
	c
)


func main() {
	fmt.Println(a, b, c)
}
```
_Output - 13 5 6_

```go
const (
	_  = iota
	KB = 1 << (10 * iota)
	MB
	GB
)

func main() {
	fileSize := 12345600000.
	fmt.Printf("%.2fKB\n%.2fMB\n%.2fGB", fileSize/KB, fileSize/MB, fileSize/GB)
}
```
_Output - 12056250.00KB 11773.68MB 11.50GB_

## Arrays
### Syntax
```go
var name = [size]Type{}
```
```go
func main() {
	colors := [3]string{"red", "green", "yellow"}
	fmt.Print(colors)
}
```
or
```go
func main() {
	colors := [...]string{"red", "green", "yellow"}
	fmt.Print(colors)
}
```
or
```go
func main() {
	var colors [3]string
	colors[0] = "red"
	colors[1] = "green"
	colors[2] = "yellow"
	fmt.Print(colors)
}
```
_Output - [red green yellow]_

**len() returns the size of an array**
```go
func main() {
	var colors [3]string
	colors[0] = "red"
	colors[1] = "green"
	colors[2] = "yellow"
	fmt.Print(colors, len(colors))
}
```
_Output - [red green yellow] 3_

### Copying
```go
func main() {
	colors := [...]string{"red", "green", "yellow"}
	newColors := colors
	newColors[1] = "black"
	fmt.Println(colors, len(colors))
	fmt.Println(newColors, len(newColors))
}
```
_Output - [red green yellow] 3 [red black yellow] 3_

### Getting pointer
```go
func main() {
	colors := [...]string{"red", "green", "yellow"}
	newColors := &colors
	newColors[1] = "black"
	fmt.Println(colors, len(colors))
	fmt.Println(*newColors, len(newColors))
}
```
_Output - [red black yellow] 3 [red black yellow] 3_

## Slices
**Slices are pointing at the same data**
```go
func main() {
	colors := []string{"red", "green", "yellow"}
	newColors := colors
	newColors[1] = "black"
	fmt.Println(colors, len(colors))
	fmt.Println(newColors, len(newColors))
}
```
_Output - [red black yellow] 3 [red black yellow] 3_

```go
func main() {
	a := []int{1, 2, 3, 4, 5, 6, 7, 8, 9, 10}
	b := a[:] // this is a slice
	c := a[3:]
	d := a[:6]
	e := a[4:6]
	fmt.Println(a)
	fmt.Println(b)
	fmt.Println(c)
	fmt.Println(d)
	fmt.Println(e)
}
```
Output

[1 2 3 4 5 6 7 8 9 10]

[1 2 3 4 5 6 7 8 9 10]

[4 5 6 7 8 9 10]

[1 2 3 4 5 6]

[5 6]

```go
func main() {
	a := []int{1, 2, 3, 4, 5, 6, 7, 8, 9, 10}
	b := a[:]
	c := a[3:]
	d := a[:6]
	e := a[4:6]
	a[2] = -1
	fmt.Println(a)
	fmt.Println(b)
	fmt.Println(c)
	fmt.Println(d)
	fmt.Println(e)
}
```
Output

[1 2 -1 4 5 6 7 8 9 10]

[1 2 -1 4 5 6 7 8 9 10]

[4 5 6 7 8 9 10]

[1 2 -1 4 5 6]

[5 6]

```go
func main() {
	a := [...]int{1, 2, 3, 4, 5, 6, 7, 8, 9, 10} // watch carefully
	b := a[:] // it's also a slice
	c := a[3:]
	d := a[:6]
	e := a[4:6]
	f := a // but it's an array
	a[2] = -1
	fmt.Println(a)
	fmt.Println(b)
	fmt.Println(c)
	fmt.Println(d)
	fmt.Println(e)
	fmt.Println(f)
}
```
Output

[1 2 -1 4 5 6 7 8 9 10]

[1 2 -1 4 5 6 7 8 9 10]

[4 5 6 7 8 9 10]

[1 2 -1 4 5 6]

[5 6]

[1 2 3 4 5 6 7 8 9 10]

## Make function
### With 2 params
#### Syntax
```go
	make([]Type, size)
```

```go
func main() {
	a := make([]int, 3)
	fmt.Println(a, len(a), cap(a))
}
```
_Output - [0 0 0] 3 3_

### With 3 params
#### Syntax
**In this case size and capactiy are similar to vec.size() and vec.capacity()**
```go
	make([]Type, size, capacity)
```

```go
func main() {
	a := make([]int, 4, 10)
	fmt.Println(a, len(a), cap(a))
}
```
_Output - [0 0 0 0] 4 10_

```go
func main() {
	a := make([]int, 4, 10)
	a = append(a, 3, 4)
	fmt.Println(a, len(a), cap(a))
}
```
_Output - [0 0 0 0 3 4] 6 10_

```go
func main() {
	a := make([]int, 4, 5)
	a = append(a, 3)
	fmt.Println(a, len(a), cap(a))
	a = append(a, 4)
	fmt.Println(a, len(a), cap(a))
}
```
Output

[0 0 0 0 3] 5 5

[0 0 0 0 3 4] 6 10

## Append function
### Syntax
```go
	append(slice []Type, elems ...Type)
```
### Examples
```go
func main() {
	a := []int{1, 2, 3, 4}
	a = append(a, 5)
	fmt.Println(a)
}
```
_Output - [1 2 3 4 5]_

```go
func main() {
	a := []int{1, 2, 3, 4}
	a = append(a, 5, -3, 2, 4)
	fmt.Println(a)
}
```
_Output - [1 2 3 4 5 -3 2 4]_

```go
func main() {
	a := []int{1, 2, 3, 4}
	b := []int{-1, -2, -3, -4}
	a = append(a, b...)
	fmt.Println(a)
}
```
_Output - [1 2 3 4 -1 -2 -3 -4]_
