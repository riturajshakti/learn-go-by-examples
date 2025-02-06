[Goto Home](../README.md)

# Printing the data type of a variable/constant

```go
x := []int{1, 2, 3}
fmt.Printf("x = %v\n", x)
fmt.Printf("Typeof x = %T\n", x)
```

**Output:**

```
x = [1 2 3]
Typeof x = []int
```

# Comparing the data type of variable in if-else/switch

## Using switch

```go
var x any
x = []int{1, 2, 3}
switch x.(type) {
case []int:
  fmt.Println("x is slice of int")
case int:
  fmt.Println("x is int")
default:
  fmt.Println("x is unknown")
}
```

**Output:**

```
x is slice of int
```

## Using Ladder if-else

```go
var x any
x = []int{1, 2, 3}
if _, ok := x.([]int); ok {
  fmt.Println("x is slice of int")
} else if _, ok = x.(int); ok {
  fmt.Println("x is int")
} else {
  fmt.Println("x is unknown")
}
```

**Output:**

```
x is slice of int
```

# Checking if a variable is an slice

```go
var x any
x = []int{1, 2, 3}
kind := reflect.TypeOf(x).Kind()
if kind == reflect.Slice {
  fmt.Println("x is slice")
} else {
  fmt.Println("x is not a slice")
}
```

**Output:**

```
x is slice
```

# Checking if a variable is a specific object

```go
type User struct {
  Name string
}

var x any
x = User{"John"}
if _, ok := x.(User); ok {
  fmt.Println("x is User")
} else {
  fmt.Println("x is not a User")
}
```

**Output:**

```
x is User
```

# Checking if a variable is a function

```go
var x any
x = func(c int) int {
  return 8
}
kind := reflect.TypeOf(x).Kind()
if kind == reflect.Func {
  fmt.Println("x is function")
} else {
  fmt.Println("x is not a function")
}
```

**Output:**

```
x is function
```

# dynamic variables

```go
var x any
x = 6
fmt.Println(x)
x = "Test"
fmt.Println(x)
x = true
fmt.Println(x)
```

**Output:**

```
6
Test
true
```


| [< Previous Page](./strings.md) | [Home Page](../README.md) | [Next Page >](./numbers.md) |
|---|---|---|
