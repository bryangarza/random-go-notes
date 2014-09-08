RANDOM GO NOTES
===============

some cute Go snippets and such.


Sep 7 2014
==========

Since the zero value of a slice (nil) acts like a zero-length slice, you can
declare a slice variable and then append to it in a loop:

```go
// Filter returns a new slice holding only
// the elements of s that satisfy f()
func Filter(s []int, fn func(int) bool) []int {
    var p []int // == nil
    for _, v := range s {
        if fn(v) {
            p = append(p, v)
        }
    }
    return p
}
```


Sep 6 2014
==========

Slices
------

A slice points to an array of values and also includes a length.

[]T is a slice with elements of type T.

```go
package main

import "fmt"

func main() {

    excellent := []string{"hi", "what", "is", "going", "on", "?"}
    fmt.Println("excellent ==", excellent)

    for i := 0; i < len(excellent); i++ {
        fmt.Printf("excellent[%d] == %v\n", i, excellent[i])
    }
    fmt.Printf("#%v\n\n", excellent)



    p := []int{2, 3, 5, 7, 11, 13}
    fmt.Println("p ==", p)

    for i := 0; i < len(p); i++ {
        fmt.Printf("p[%d] == %d\n", i, p[i])
    }
    fmt.Printf("%#v\n", p)

}
```

The output:

```
excellent == [hi what is going on ?]
excellent[0] == hi
excellent[1] == what
excellent[2] == is
excellent[3] == going
excellent[4] == on
excellent[5] == ?
#[hi what is going on ?]

p == [2 3 5 7 11 13]
p[0] == 2
p[1] == 3
p[2] == 5
p[3] == 7
p[4] == 11
p[5] == 13
[]int{2, 3, 5, 7, 11, 13}
```


Sep 5 2014
==========

Go Homebrew Caveats
-------------------

As of go 1.2, a valid GOPATH is required to use the `go get` command:
  http://golang.org/doc/code.html#GOPATH

`go vet` and `go doc` are now part of the go.tools sub repo:
  http://golang.org/doc/go1.2#go_tools_godoc

To get `go vet` and `go doc` run:
  go get code.google.com/p/go.tools/cmd/godoc
  go get code.google.com/p/go.tools/cmd/vet

You may wish to add the GOROOT-based install location to your PATH:
  export PATH=$PATH:/usr/local/opt/go/libexec/bin

Bash completion has been installed to:
  /usr/local/etc/bash_completion.d

zsh completion has been installed to:
  /usr/local/share/zsh/site-functions


Go's basic types:
-----------------

bool

string

int  int8  int16  int32  int64
uint uint8 uint16 uint32 uint64 uintptr

byte // alias for uint8

rune // alias for int32
     // represents a Unicode code point

float32 float64

complex64 complex128


Newton's sqrt method (A Tour of Go Pt. 25):
-------------------------------------------------------

```go
package main

import (
    "fmt"
    "math"
)

const delta = 0.001

func Sqrt(x float64) float64 {
    z := x / 2.0

    for {
        z -= ((z * z) - x) / (2 * z)
        zsq := z * z

        if math.Abs(zsq - x) < delta {
            return z
        }
    }
}

func main() {
    num := float64(64)
    fmt.Printf("square root of %2v: %.4f\n", num, Sqrt(num))
}
```
