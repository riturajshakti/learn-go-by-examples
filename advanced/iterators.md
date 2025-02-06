[Goto Home](../README.md)

# Iterators

```go
package main

import (
  "fmt"
)

func main() {
  s := []string{"red", "green", "blue"}
  for i, e := range Backward(s) {
    fmt.Println(i, e)
  }
}

func Backward[T any](s []T) func(func(int, T) bool) {
  return func(yield func(int, T) bool) {
    for i := len(s) - 1; i >= 0; i-- {
      if !yield(i, s[i]) {
        return
      }
    }
  }
}
```

**Output:**

```
2 blue
1 green
0 red
```

|  |  |  |
| --- | --- | --- |
| [< Previous Page](./os.md) | [Home Page](../README.md) | [Next Page >](./generics.md) |
|  |  |  |
