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
