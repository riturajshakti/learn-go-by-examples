[Goto Home](../README.md)

# returning multiple values from a function

```go
func main() {
  area, err := Area(7)
  if err != nil {
    fmt.Println(err)
  } else {
    fmt.Println(area)
  }

  area, err = Area(-7)
  fmt.Println(area, err)
}

func Area(radius float64) (float64, error) {
  if radius <= 0 {
    return 0, fmt.Errorf("radius must be positive")
  }
  return math.Pi * radius * radius, nil
}
```

**Output:**

```
153.93804002589985
0 radius must be positive
```

# creating function with unlimited parameters

```go
func main() {
  Log(3, true, "Test")
}

func Log(values ...any) {
  for _, e := range values {
    fmt.Println(e)
  }
}
```

**Output:**

```
3
true
Test
```

# passing an array elements to a function with unlimited params

```go
func main() {
  Log(3, true, "Test")
}

func Log(values ...any) {
  fmt.Println(values...)
}
```

**Output:**

```
3 true Test
```

# creating anonymous functions

```go
square := func(n int) int { return n * n }
fmt.Println(square(3))
```

**Output:**

```
9
```

# self invoking function

```go
square := func(n int) int { return n * n }(10)
fmt.Println(square)
```

**Output:**

```
100
```

# creating closures which manages states

**Counter Example:**

```go
func main() {
  adder := Counter()
  fmt.Println(adder())
  fmt.Println(adder())
  fmt.Println(adder())
}

func Counter() func() int {
  sum := 0
  adder := func() int {
    sum++
    return sum
  }
  return adder
}
```

**Output:**

```
1
2
3
```

**Multiple Operations:**

```go
type User struct {
  Name    string
  Age     int
  Married bool
}

type ActionResult struct {
  user           User
  showDetails    func()
  incrementAge   func() int
  toggleMarriage func()
  changeName     func(string)
}

func main() {
  actions := Actions("Raj", 20, false)
  fmt.Println(actions.user)
  actions.showDetails()
  actions.incrementAge()
  actions.showDetails()
  actions.toggleMarriage()
  actions.showDetails()
  actions.changeName("John")
  actions.showDetails()
}

func Actions(name string, age int, married bool) ActionResult {
  user := User{name, age, married}
  showDetails := func() {
    fmt.Printf("Name: %s, Age: %d, Married: %t\n", user.Name, user.Age, user.Married)
  }
  incrementAge := func() int {
    user.Age++
    fmt.Println("Age increased")
    return user.Age
  }
  toggleMarriage := func() {
    user.Married = !user.Married
    fmt.Println("Marriage toggled")
  }
  changeName := func(name string) {
    user.Name = name
    fmt.Println("Name changed")
  }
  return ActionResult{user, showDetails, incrementAge, toggleMarriage, changeName}
}
```

**Output:**

```
{Raj 20 false}
Name: Raj, Age: 20, Married: false
Age increased
Name: Raj, Age: 21, Married: false
Marriage toggled
Name: Raj, Age: 21, Married: true
Name changed
Name: John, Age: 21, Married: true
```

# Higher Order Function: Map

```go
func main() {
  numbers := []int{1, 2, 3}
  stringSquares := Map(numbers, func(e, i int) string {
    return fmt.Sprintf("%d", e*e)
  })
  fmt.Println(stringSquares)
  fmt.Printf("%T\n", stringSquares[0])
}

func Map[T any, R any](list []T, f func(e T, i int) R) []R {
  s := make([]R, len(list))
  for i, e := range list {
    s[i] = f(e, i)
  }
  return s
}
```

**Output:**

```
[1 4 9]
string
```

# Higher Order Function: Filter

```go
func main() {
  numbers := []int{1, 2, 3, 4, 5, 6}
  evens := Filter(numbers, func(e, i int) bool {
    return e%2 == 0
  })
  fmt.Println(evens)
}

func Filter[T any](list []T, f func(e T, i int) bool) []T {
  s := []T{}
  for i, e := range list {
    if f(e, i) {
      s = append(s, e)
    }
  }
  return s
}
```

**Output:**

```
[2 4 6]
```

# Higher Order Function: Sort

```go
type User struct {
  Name string
  Age  int
  At   time.Time
}

func main() {
  numbers := []int{2, 1, 5, 3, 6, 4, 8, 7}
  sorted := Sort(numbers, func(a, b int) int {
    return a - b
  })
  fmt.Println("Sorted Numbers:", sorted)
  fmt.Println("-----------")

  users := []User{
    {"Amy", 34, Parse("2025-02-04T11:23:00Z")},
    {"John", 12, Parse("2021-01-02T12:00:00Z")},
    {"Zac", 37, Parse("2027-09-24T06:34:34Z")},
  }

  sortedByName := Sort(users, func(a, b User) int {
    return strings.Compare(a.Name, b.Name)
  })
  fmt.Println("Sorted by name:")
  for _, e := range sortedByName {
    fmt.Println(e)
  }
  fmt.Println("-----------")

  sortedByAge := Sort(users, func(a, b User) int {
    return a.Age - b.Age
  })
  fmt.Println("Sorted by age in descending:")
  for _, e := range sortedByAge {
    fmt.Println(e)
  }
  fmt.Println("-----------")

  sortedByDate := Sort(users, func(a, b User) int {
    return a.At.Compare(b.At)
    // or use this:
    // return int(a.At.UnixMilli() - b.At.UnixMilli())
  })
  fmt.Println("Sorted by date:")
  for _, e := range sortedByDate {
    fmt.Println(e)
  }
}

func Parse(s string) time.Time {
  d, _ := time.Parse(time.RFC3339, s)
  return d
}

func Sort[T any](list []T, f func(a, b T) int) []T {
  s := make([]T, len(list))
  copy(s, list)
  for i := 0; i < len(s)-1; i++ {
    for j := 0; j < len(s)-i-1; j++ {
      if f(s[j], s[j+1]) > 0 {
        s[j], s[j+1] = s[j+1], s[j]
      }
    }
  }
  return s
}
```

**Output:**

```
Sorted Numbers: [1 2 3 4 5 6 7 8]
-----------
Sorted by name:
{Amy 34 2025-02-04 11:23:00 +0000 UTC}
{John 12 2021-01-02 12:00:00 +0000 UTC}
{Zac 37 2027-09-24 06:34:34 +0000 UTC}
-----------
Sorted by age in descending:
{John 12 2021-01-02 12:00:00 +0000 UTC}
{Amy 34 2025-02-04 11:23:00 +0000 UTC}
{Zac 37 2027-09-24 06:34:34 +0000 UTC}
-----------
Sorted by date:
{John 12 2021-01-02 12:00:00 +0000 UTC}
{Amy 34 2025-02-04 11:23:00 +0000 UTC}
{Zac 37 2027-09-24 06:34:34 +0000 UTC}
```

# Higher Order Function: ForEach

```go
func main() {
  names := []string{"Amy", "John", "Paul"}
  ForEach(names, func(e string, i int) { fmt.Println(i, e) })
}

func ForEach[T any](list []T, f func(e T, i int)) {
  for i, e := range list {
    f(e, i)
  }
}
```

**Output:**

```
0 Amy
1 John
2 Paul
```

# Higher Order Function: Some/Any

```go
func main() {
  names := []string{"Amy", "John", "Paul"}
  anyVowelName := Any(names, func(e string, i int) bool {
    return strings.Contains("aeiouAEIOU", string(e[0]))
  })
  fmt.Println("Any name starts with Vowel:", anyVowelName)
}

func Any[T any](list []T, f func(e T, i int) bool) bool {
  for i, e := range list {
    if f(e, i) {
      return true
    }
  }
  return false
}
```

**Output:**

```
Any name starts with Vowel: true
```

# Higher Order Function: Every

```go
func main() {
  names := []string{"Amy", "John", "Paul"}
  everyVowelName := Every(names, func(e string, i int) bool {
    return strings.Contains("aeiouAEIOU", string(e[0]))
  })
  fmt.Println("Every name starts with Vowel:", everyVowelName)
}

func Every[T any](list []T, f func(e T, i int) bool) bool {
  for i, e := range list {
    if !f(e, i) {
      return false
    }
  }
  return true
}
```

**Output:**

```
Every name starts with Vowel: false
```

# Higher Order Function: Find

```go
func main() {
  names := []string{"Amy", "John", "Paul"}
  vowel, err := Find(names, func(e string, i int) bool {
    return strings.Contains("aeiouAEIOU", string(e[0]))
  })
  if err == nil {
    fmt.Println("Vowel name:", vowel)
  }
}

func Find[T any](list []T, f func(e T, i int) bool) (T, error) {
  for i, e := range list {
    if f(e, i) {
      return e, nil
    }
  }
  return list[0], fmt.Errorf("Not found")
}
```

**Output:**

```
Vowel name: Amy
```

# Higher Order Function: FindIndex

```go
func main() {
  names := []string{"Amy", "John", "Paul"}
  vowelIndex := FindIndex(names, func(e string, i int) bool {
    return strings.Contains("aeiouAEIOU", string(e[0]))
  })
  fmt.Println("Vowel name index:", vowelIndex)
}

func FindIndex[T any](list []T, f func(e T, i int) bool) int {
  for i, e := range list {
    if f(e, i) {
      return i
    }
  }
  return -1
}
```

**Output:**

```
Vowel name index: 0
```

# Higher Order Function: Reduce

```go
func main() {
  numbers := []int{1, 2, 3, 4, 5}
  sum := Reduce(numbers, 0, func(acc, e, i int) int {
    return acc + e
  })
  fmt.Println("Sum:", sum)

  product := Reduce(numbers, 1, func(acc, e, i int) int {
    return acc * e
  })
  fmt.Println("Product:", product)
}

func Reduce[T, U any](list []T, initial U, f func(acc U, e T, i int) U) U {
  result := initial
  for i, e := range list {
    result = f(result, e, i)
  }
  return result
}
```

**Output:**

```
Sum: 15
Product: 120
```

# Higher Order Function: Group

```go
func main() {
  numbers := []int{1, 2, 3, 4, 5, 6, 7, 8}
  rules := map[string]func(e, i int) bool{
    "even": func(e, i int) bool { return e%2 == 0 },
    "odd":  func(e, i int) bool { return e%2 == 1 },
  }

  grouped := Group(numbers, rules)
  fmt.Println("Grouped:", grouped)
}

func Group[T any](list []T, rules map[string]func(e T, i int) bool) map[string][]T {
  result := map[string][]T{}
  for rule, fn := range rules {
    result[rule] = []T{}
    for i, e := range list {
      if fn(e, i) {
        result[rule] = append(result[rule], e)
      }
    }
  }
  return result
}
```

**Output:**

```
Grouped: map[even:[2 4 6 8] odd:[1 3 5 7]]
```


| [< Previous Page](./conditionals-loops.md) | [Home Page](../README.md) | [Next Page >](./json.md) |
|---|---|---|
