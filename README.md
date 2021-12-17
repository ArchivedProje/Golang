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
### Bitwise operations
```go
package main

import "fmt"

func main() {
	var a uint8 = 10 // 00001010
	var b uint8 = 12 // 00001100
	fmt.Println(a & b) // a and b = 00001000 = 8
	fmt.Println(a | b) // a or b = 00001110 = 14
	fmt.Println(a ^ b) // a xor b = 00000110 = 6
	fmt.Println(a &^ b) // a and not b = 00001010 & 11110011 = 00000010 = 2
	fmt.Println(a |^ b) // a or not b =  00001010 | 11110011 = 11111011 = 251
	fmt.Println(a ^^ b) // a xor not b = 00001010 ^ 11110011 = 11111001 = 249
}
```
