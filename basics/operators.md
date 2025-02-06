[Goto Home](../README.md)

# Increment/Decrement Operators

```go
n := 9
n++
fmt.Println(n)
n--
fmt.Println(n)
```

**Output:**

```
10
9
```

# Conditional Operators

```go
func main() {
  msg := Conditional(4 < 3, "4 is smaller", "4 is larger")
  fmt.Println(msg)
}

func Conditional[T any](condition bool, truthy T, falsy T) T {
  if condition {
    return truthy
  } else {
    return falsy
  }
}
```

**Output:**

```
4 is larger
```


| [< Previous Page](./regex.md) | [Home Page](../README.md) | [Next Page >](./datetime.md) |
|---|---|---|
