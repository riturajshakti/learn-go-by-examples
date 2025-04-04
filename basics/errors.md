# Errors

| [🏠Goto Home](../README.md) | [Goto Bottom🔻](#navigations) |
|---|---|

# Topics

- [exit a program (throwing errors)](#exit-a-program-throwing-errors)
- [prevent a program from exit](#prevent-a-program-from-exit)

## exit a program (throwing errors)

```go
func main() {
  panic("exiting")
}
```

**Output:**

```
panic: exiting

goroutine 1 [running]:
main.main()
        C:/Users/ritur/Desktop/My_Works/Learn/Go/go-tutorial/main.go:4 +0x25
```

## prevent a program from exit

```go
func main() {
  defer func() {
    if r := recover(); r != nil {
      fmt.Println("Recovered here:", r)
    }
  }()
  panic("exiting")
}
```

**Output:**

```
Recovered here: exiting
```

# Navigations

| [< Previous Page](./json.md) | [Home Page](../README.md) | [Next Page >](./concurrency.md) |
|---|---|---|
