RANDOM GO NOTES
===============

some cute Go snippets and such.


Go Homebrew Caveats
-------------------

As of go 1.2, a valid GOPATH is required to use the `go get` command:
  http://golang.org/doc/code.html#GOPATH

`go vet` and `go doc` are now part of the go.tools sub repo:
  http://golang.org/doc/go1.2#go_tools_godoc

To get `go vet` and `go doc` run:
  `go get code.google.com/p/go.tools/cmd/godoc`
  `go get code.google.com/p/go.tools/cmd/vet`

You may wish to add the GOROOT-based install location to your PATH:
  `export PATH=$PATH:/usr/local/opt/go/libexec/bin`

Bash completion has been installed to:
  `/usr/local/etc/bash_completion.d`

zsh completion has been installed to:
  `/usr/local/share/zsh/site-functions`


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


Newton's method for square roots (A Tour of Go Pt. 25):
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
