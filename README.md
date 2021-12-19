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
