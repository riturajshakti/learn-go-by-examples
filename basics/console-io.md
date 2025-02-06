[Goto Home](../README.md)

# Print a string on console output

```go
fmt.Println("Hello world")
```

**Output:**

```
Hello world
```

# Print a formatted string on console output

```go
married, age, name, score := false, 29, "raj", 78.50
fmt.Printf("Married: %t, Age: %d, Name: %s, Score: %g\n", married, age, name, score)
```

**Output:**

```
Married: false, Age: 29, Name: raj, Score: 78.5
```

# Print a string on console error

```go
fmt.Fprintf(os.Stderr, "Error message\n")
```

**Output:**

```
Error message
```

# Print a string without newline character at the end

```go
fmt.Print("Hello world")
```

**Output:**

```
Hello world
```

# Scan a string from console input

```go
package main

import (
	"bufio"
	"fmt"
	"os"
)

func main() {
	reader := bufio.NewReader(os.Stdin)
	fmt.Print("Enter a string: ")
	s, _ := reader.ReadString('\n')
	fmt.Println("String is:", s)
}
```

**Output:**

```
Enter a string: Hello world
String is: Hello world
```

# Scan numbers and bool from console input

```go
// Scanning numbers
var n, m int
fmt.Print("Enter numbers: ")
fmt.Scanf("%d %d\n", &n, &m)
fmt.Println("Numbers are: ", n, m)

// Scanning bool value
var ok bool
fmt.Print("Enter bool value: ")
fmt.Scanf("%t", &ok)
fmt.Println("Value is:", ok)
```

**Output:**

```
Enter numbers: 4 5 
Numbers are:  4 5
Enter bool value: true
Value is: true
```
