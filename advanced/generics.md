[Goto Home](../README.md)

# Basic Generic Function

```go
package main

import (
	"fmt"
)

func main() {
	colors := []string{"red", "green", "blue"}
	fmt.Println("Colors:", colors)
	colorsLength := Map(colors, func(e string, i int) int {
		return len(e)
	})
	fmt.Println("Colors length:", colorsLength)
	fmt.Println()

	numbers := []int{1, 2, 3, 4, 5}
	fmt.Println("Numbers:", numbers)
	squares := Map(numbers, func(e, i int) int {
		return e * e
	})
	fmt.Println("Squares:", squares)
}

func Map[T, U any](s []T, f func(e T, i int) U) []U {
	r := make([]U, len(s))
	for i, e := range s {
		r[i] = f(e, i)
	}
	return r
}
```

**Output:**

```
Colors: [red green blue]
Colors length: [3 5 4]

Numbers: [1 2 3 4 5]
Squares: [1 4 9 16 25]
```
