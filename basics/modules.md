# Modules

| [🏠Goto Home](../README.md) | [Goto Bottom🔻](#navigations) |
|---|---|

# Topics

- [Creating & Using Package](#creating--using-package)

## Creating & Using Package

```go
// utils/utils.go
package utils

func Sum(values ...int) int {
  total := 0
  for _, e := range values {
    total += e
  }
  return total
}


// main.go
package main

import (
  "fmt"

  "github.com/riturajshakti/go-examples/utils"
)

func main() {
  sum := utils.Sum(1, 2, 3, 4, 5)
  fmt.Println("Sum =", sum)
}
```

**Output:**

```
Sum = 15
```

# Navigations

| [< Previous Page](./concurrency.md) | [Home Page](../README.md) | [Next Page >](./oops.md) |
|---|---|---|
