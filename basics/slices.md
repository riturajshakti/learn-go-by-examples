[Goto Home](../README.md)

# List of dynamic data types

```go
var list []any
list = []any{true, 34, "John", []int{1, 2, 3}, map[string]int{"A": 65, "a": 97, "0": 48}}
fmt.Println(list)
```

**Output:**

```
[true 34 John [1 2 3] map[0:48 A:65 a:97]]
```

# Creating static list

```go
var list [3]any
list = [3]any{true, 34, "John"}
fmt.Println(list)
```

**Output:**

```
[true 34 John]
```

# Creating dynamic list

```go
var list []int
list = []int{1, 2, 3}
list = append(list, 4)
fmt.Println(list)
```

**Output:**

```
[1 2 3 4]
```

# Creating list for any type of map

```go
list := []map[string]any{
  {
    "name":    "John",
    "age":     23,
    "married": false,
  },
  {
    "name":    "Elisa",
    "age":     25,
    "married": true,
  },
  {
    "name":    "Henry",
    "age":     28,
    "married": false,
  },
}
for _, e := range list {
  fmt.Println(e)
}
```

**Output:**

```
map[age:23 married:false name:John]
map[age:25 married:true name:Elisa]
map[age:28 married:false name:Henry]
```

# Getting list size

```go
list := []string{"ABC", "DEF", "GHI", "JKL"}
size := len(list)
fmt.Println(size)
```

**Output:**

```
4
```

# Accessing list element at specific index

```go
list := []string{"ABC", "DEF", "GHI", "JKL"}
fmt.Println(list[0], list[1])
```

**Output:**

```
ABC DEF
```

# Updating list element at specific index

```go
list := []string{"ABC", "DEF", "GHI", "JKL"}
list[0] = "ZZZ"
fmt.Println(list[0])
```

**Output:**

```
ZZZ
```

# Removing list element at specific index

```go
list := []string{"ABC", "DEF", "GHI", "JKL"}
fmt.Println(list)

n := 2
c := append(list[0:n], list[n+1:]...)
fmt.Printf("Deleted at n(%d): %v\n", n, c)
```

**Output:**

```
[ABC DEF GHI JKL]
Deleted at n(2): [ABC DEF JKL]
```

# Traversing a list

```go
list := []string{"ABC", "DEF", "GHI", "JKL"}
for i, e := range list {
  fmt.Println(i, e)
}
```

**Output:**

```
0 ABC
1 DEF
2 GHI
3 JKL
```

# Comparing 2 lists based on their contents

**1st method:** Using custom function (Shallow check only)

```go
func main() {
  list1 := []string{"ABC", "DEF", "GHI", "JKL"}
  list2 := []string{"ABC", "DEF", "GHI", "JKL"}

  if isEqual(list1, list2) {
    fmt.Println("list1 equals list2")
  } else {
    fmt.Println("list1 not equals list2")
  }
}

func isEqual[T comparable](list1, list2 []T) bool {
  if len(list1) != len(list2) {
    return false
  }
  for i := range len(list1) {
    if list1[i] != list2[i] {
      return false
    }
  }
  return true
}
```

**Output:**

```
list1 equals list2
```

**2nd method:** Using json marshal & unmarshal (Deep check)

```go
list1 := []string{"ABC", "DEF", "GHI", "JKL"}
list2 := []string{"ABC", "DEF", "GHI", "JKL"}

s1, _ := json.Marshal(list1)
s2, _ := json.Marshal(list2)

if string(s1) == string(s2) {
  fmt.Println("list1 equals list2")
} else {
  fmt.Println("list1 not equals list2")
}
```

**Output:**

```
list1 equals list2
```

# joining slice elements in a string

```go
list := []string{"ABC", "DEF", "GHI"}
fmt.Println(strings.Join(list, ""))
```

**Output:**

```
ABCDEFGHI
```

# joining slice elements using custom string

```go
list := []string{"ABC", "DEF", "GHI"}
fmt.Println(strings.Join(list, "-"))
```

**Output:**

```
ABC-DEF-GHI
```

# check if an element exist in an array

```go
list := []string{"ABC", "DEF", "GHI"}
if slices.Contains(list, "GHI") {
  fmt.Println("list contains GHI")
} else {
  fmt.Println("list does not contains GHI")
}
```

**Output:**

```
list contains GHI
```

# find element's index in an array

```go
list := []string{"ABC", "DEF", "GHI"}
index := slices.Index(list, "GHI")
fmt.Println("Index of GHI:", index)
```

**Output:**

```
2
```

# find element's index from last in a slice

```go
list := []string{"A", "B", "A", "C"}
index := -1
for i := len(list) - 1; i >= 0; i-- {
  if list[i] == "A" {
    index = i
    break
  }
}
fmt.Println("Last Index of A:", index)
```

**Output:**

```
2
```

# inserting elements in a slice from end

```go
list := []string{"A", "B", "C"}
list = append(list, "D")
fmt.Println(list)
```

**Output:**

```
[A B C D]
```

# inserting elements in a slice from start

```go
list := []string{"B", "C", "D"}
list = append([]string{"A"}, list...)
fmt.Println(list)
```

**Output:**

```
[A B C D]
```

# inserting elements in a slice at specific index

```go
old := []string{"A", "B", "D"}
index := 2
new := append([]string{}, old[0:index]...)
new = append(new, "C")
new = append(new, old[index:]...)
fmt.Println(new)
```

**Output:**

```
[A B C D]
```

# removing n number of elements in a slice at specific index

```go
old := []string{"A", "B", "C", "D", "E", "F"}
index, count := 2, 3
new := append([]string{}, old[0:index]...)
new = append(new, old[index+count:]...)
fmt.Println(new)
```

**Output:**

```
[A B F]
```

# removing an element from last in a slice

```go
old := []string{"A", "B", "C", "D"}
new := append([]string{}, old[0:len(old)-1]...)
fmt.Println(new)
```

**Output:**

```
[A B C]
```

# reversing a slice

**1st method:** Efficient method

```go
old := []string{"A", "B", "C", "D"}
new := make([]string, len(old))
for i := range len(old) {
  new[i] = old[len(old)-i-1]
}
fmt.Println(new)
```

**Output:**

```
[D C B A]
```

**2nd method:** Not so efficient but readable

```go
old := []string{"A", "B", "C", "D"}
new := []string{}
for _, e := range old {
  new = append([]string{e}, new...)
}
fmt.Println(new)
```

**Output:**

```
[D C B A]
```

# Clearing the list

```go
list := []string{"A", "B", "C", "D"}
list = []string{}
fmt.Println(list)
```

**Output:**

```
[]
```

# shuffle a list

```go
list := []string{"A", "B", "C", "D"}
for i := 0; i < len(list); i++ {
  r := rand.Intn(len(list))
  list[i], list[r] = list[r], list[i]
}
fmt.Println(list)
```

**Output:**

```
[B C D A]
```

# Multi-dimensional slice (Nested slices)

```go
points := [][]float64{
  {1, 2},
  {2.3, 4},
  {-4, 5},
  {0, 0},
}
for i, e := range points {
  fmt.Println(i, e)
}
```

**Output:**

```
0 [1 2]
1 [2.3 4]
2 [-4 5]
3 [0 0]
```

# Traversing a multi-dimensional slice

```go
points := [][]float64{
  {1, 2, 3},
  {2.3, 4, 5},
  {-4, 5, 0},
  {0, 0, 0},
}
for _, e := range points {
  for _, f := range e {
    fmt.Printf("%g, ", f)
  }
  fmt.Println()
}
```

**Output:**

```
1, 2, 3, 
2.3, 4, 5,
-4, 5, 0,
0, 0, 0,
```

# Concatenating 2 slices into one

```go
a := []int{1, 2, 3}
b := []int{4, 5, 6}
c := append(a, b...)
fmt.Println(c)
```

**Output:**

```
[1 2 3 4 5 6]
```

# Removing duplicates from an array

```go
func main() {
  list := []int{1, 2, 1, 3, 2, 1, 4, 2, 1}
  list = RemoveDuplicates(list)
  fmt.Println(list)
}

func RemoveDuplicates[T comparable](list []T) []T {
  m := map[T]bool{}
  for _, e := range list {
    if _, ok := m[e]; !ok {
      m[e] = true
    }
  }
  s := []T{}
  for k := range m {
    s = append(s, k)
  }
  return s
}
```

**Output:**

```
[1 2 3 4]
```

# shallow clone an array

```go
list := []int{1, 2, 3, 4, 5}
cloned := make([]int, len(list))
copy(cloned, list)
fmt.Println(cloned)
```

**Output:**

```
[1 2 3 4 5]
```

# deep clone a slice

```go
list := []int{1, 2, 3, 4, 5}
var cloned []int
s, _ := json.Marshal(list)
json.Unmarshal(s, &cloned)
fmt.Println(cloned)
```

**Output:**

```
[1 2 3 4 5]
```


| [< Previous Page](./numbers.md) | [Home Page](../README.md) | [Next Page >](./maps.md) |
|---|---|---|
