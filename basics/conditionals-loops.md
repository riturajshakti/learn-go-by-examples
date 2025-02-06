[Goto Home](../README.md)

# Switch where multiple cases executes same statement

```go
x := 3
switch x {
case 1 | 2 | 3:
  fmt.Println("x is either 1, 2 or 3")
default:
  fmt.Println("x is something else")
}
```

**Output:**

```
x is either 1, 2 or 3
```

# Reverse for loop on numbers

```go
for i := 10; i > 0; i-- {
  fmt.Printf("%d ", i)
}
```

**Output:**

```
10 9 8 7 6 5 4 3 2 1 
```

# do-while operations using while loop

```go
i := 1
for {
  fmt.Printf("%d ", i)
  i++
  if i == 4 {
    break
  }
}
```

**Output:**

```
1 2 3 
```

# for-each loop on arrays/string

For loop on slice

```go
list := []string{"John", "Kevin", "Henry"}
for _, e := range list {
  fmt.Println(e)
}
```

**Output:**

```
John
Kevin
Henry
```

For loop on string

```go
s := "ABC"
for _, e := range s {
  fmt.Println(string(e))
}
```

**Output:**

```
A
B
C
```

# for-each loop on maps

```go
m := map[string]any{
  "name":    "John",
  "age":     20,
  "married": false,
}
for k, v := range m {
  fmt.Println(k, v)
}
```

**Output:**

```
name John
age 20
married false
```

# For loop on number

```go
for i := range 3 {
  fmt.Println(i)
}
```

**Output:**

```
0
1
2
```
