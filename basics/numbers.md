# Numbers

| [🏠Goto Home](../README.md) | [Goto Bottom🔻](#navigations) |
|---|---|

# Topics

- [Create a numeric variable of 1 byte](#create-a-numeric-variable-of-1-byte)
- [finding min between many numbers](#finding-min-between-many-numbers)
- [finding max between many numbers](#finding-max-between-many-numbers)
- [rounding a number to integer](#rounding-a-number-to-integer)
- [rounding a number to `n` digits after decimal points](#rounding-a-number-to-n-digits-after-decimal-points)
- [finding random number from 0 to 1 (including 0 but excluding 1)](#finding-random-number-from-0-to-1-including-0-but-excluding-1)
- [finding random integer from a to b](#finding-random-integer-from-a-to-b)
- [floor of a number](#floor-of-a-number)
- [ceiling of a number](#ceiling-of-a-number)
- [finding a^b](#finding-ab)
- [finding nth root of a number](#finding-nth-root-of-a-number)
- [converting a number to string](#converting-a-number-to-string)
- [converting a string to number](#converting-a-string-to-number)
- [checking if a numeric string is invalid number (NaN)](#checking-if-a-numeric-string-is-invalid-number-nan)

## Create a numeric variable of 1 byte

```go
var x byte
x = 255
x++
fmt.Println(x)
```

**Output:**

```
0
```

## finding min between many numbers

**Using Custom Types**

```go
package main

import (
  "fmt"
)

func main() {
  fmt.Println(Min(2, 4, -6, 6))
}

type Ordered interface {
  ~int | ~int8 | ~int16 | ~int32 | ~int64 |
    ~uint | ~uint8 | ~uint16 | ~uint32 | ~uint64 | ~uintptr |
    ~float32 | ~float64 |
    ~string
}

func Min[T Ordered](values ...T) T {
  min := values[0]
  for _, e := range values {
    if e < min {
      min = e
    }
  }
  return min
}
```

**Output:**

```
-6
```

## finding max between many numbers

**Using package `constraints`**

Make sure to first run this command and install this package

```sh
go get golang.org/x/exp/constraints
```

```go
package main

import (
  "fmt"

  "golang.org/x/exp/constraints"
)

func main() {
  fmt.Println(Max(2, 44, -6, 6.8))
}

func Max[T constraints.Ordered](values ...T) T {
  max := values[0]
  for _, e := range values {
    if e > max {
      max = e
    }
  }
  return max
}
```

**Output:**

```
44
```

## rounding a number to integer

```go
x := 45.678
fmt.Println(math.Round(x))
```

**Output:**

```
46
```

## rounding a number to `n` digits after decimal points

```go
x := 45.678
n := 2.0
power := math.Pow(10, n)
rounded := math.Round(x*power) / power
fmt.Println(rounded)
```

**Output:**

```
45.68
```

## finding random number from 0 to 1 (including 0 but excluding 1)

```go
for range 5 {
  random := rand.Float64()
  fmt.Println(random)
}
```

**Output:**

```
0.8257985521413678
0.9714876836775942
0.2624964117023951
0.04634574032902068
0.29721240683366645
```

## finding random integer from a to b

```go
a, b := 5, 10
for range 5 {
  random := rand.Intn(b-a+1) + a
  fmt.Println(random)
}
```

**Output:**

```
7 5 8 8 10
```

## floor of a number

```go
n := 45.678
fmt.Println(math.Floor(n))
n = -45.678
fmt.Println(math.Floor(n))
```

**Output:**

```
45
-46
```

## ceiling of a number

```go
n := 45.678
fmt.Println(math.Ceil(n))
n = -45.678
fmt.Println(math.Ceil(n))
```

**Output:**

```
46
-45
```

## finding a^b

```go
fmt.Println(math.Pow(2, 5))
```

**Output:**

```
32
```

## finding nth root of a number

```go
x, n := 1024.0, 10.0
fmt.Println(math.Pow(x, 1/n))
```

**Output:**

```
2
```

## converting a number to string

```go
n := 45.6
s := fmt.Sprintf("%g", n)
fmt.Println(s)
```

**Output:**

```
45.6
```

## converting a string to number

```go
n := "45.6"
s, _ := strconv.ParseFloat(n, 64)
fmt.Println(s)
```

**Output:**

```
45.6
```

## checking if a numeric string is invalid number (NaN)

```go
n := "45.6abc"
f, err := strconv.ParseFloat(n, 64)
if err != nil {
  fmt.Println(err)
} else {
  fmt.Println(f)
}
```

**Output:**

```
45.6
```

# Navigations

| [< Previous Page](./data-types.md) | [Home Page](../README.md) | [Next Page >](./slices.md) |
|---|---|---|
