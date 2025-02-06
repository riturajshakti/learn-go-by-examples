[Goto Home](../README.md)

# Creating a regex from string

```go
s := "The quick brown fox jumps over the lazy dog"
regex := regexp.MustCompile("fox")
if regex.Match([]byte(s)) {
  fmt.Println("Fox found")
} else {
  fmt.Println("Fox not found")
}
```

**Output:**

```
Fox found
```

# Creating a regex from string with options e.g. `g`, `i`, ...

```go
s := "The quick brown fox jumps over the lazy dog"
regex := regexp.MustCompile("(?i)Fox")
if regex.Match([]byte(s)) {
  fmt.Println("Fox found")
} else {
  fmt.Println("Fox not found")
}
```

**Output:**

```
Fox found
```

# Checking if a string follows a regex

```go
s := "The quick brown fox jumps over the lazy dog"
regex := regexp.MustCompile("fox")
if regex.Match([]byte(s)) {
  fmt.Println("Fox found")
} else {
  fmt.Println("Fox not found")
}
```

**Output:**

```
Fox found
```

# Finding all matching substrings from a string with given regex

```go
s := "The quick brown fox jumps over the lazy dog"
regex := regexp.MustCompile("(?i)The")
list := regex.FindAll([]byte(s), -1)
fmt.Println(string(list[0]))
fmt.Println(string(list[1]))
```

**Output:**

```
The
the
```


| [< Previous Page](./maps.md) | [Home Page](../README.md) | [Next Page >](./operators.md) |
|---|---|---|
