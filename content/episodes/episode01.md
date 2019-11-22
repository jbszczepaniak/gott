---
title: "#01 - Go gives you static types without bureaucracy!"
date: 2018-12-30
---

## [get pdf here](/gott/episode01.pdf) 🖨

{{< highlight go >}}
package main

func main() {
    var i int = 1 // you can declare a variable with type
    var j = 2  // but you don’t have to, compiler will know
    var x, y, z = "three", "at", "once" // you can initialize many variables at a time

     // Most probably you will not frequently use var keyword.
    simplestInt := 3
    simplestString := "hey!"
    simplestBoolean := true
    simplestFloat64 := 3.14

    // And these are zero-valued variables, declared but uninitialized, they will get zero-value of a type.
    var zeroValueInt int       // 0
    var zeroValueString string // “”
    var zeroValueBoolean bool  // false
}
{{< / highlight >}}
Note that code above is completely valid in terms of syntax but it will not compile because there are variables that are not used.

Code will not compile as well if you will import a library and you will not use it.

Also in go, you don’t fight with colleagues on code review about code style because in go there is  `go fmt` tool which formats code for you!

Did you know that Rob Pike and Ken Thompson not only created Golang, but also they are inventors of UTF-8 encoding?
