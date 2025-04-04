# Strings

| [🏠Goto Home](../README.md) | [Goto Bottom🔻](#navigations) |
|---|---|

# Topics

- [Single line strings](#single-line-strings)
- [Multiline strings](#multiline-strings)
- [Template Literals/String Interpolation](#template-literalsstring-interpolation)
- [Formatted strings](#formatted-strings)
- [Accessing the character of string at specific index](#accessing-the-character-of-string-at-specific-index)
- [Traversing through a string](#traversing-through-a-string)
- [Comparing 2 strings](#comparing-2-strings)
- [Getting string size](#getting-string-size)
- [Concatenating strings](#concatenating-strings)
- [Reversing a string](#reversing-a-string)
- [Converting a string character into ASCII code](#converting-a-string-character-into-ascii-code)
- [Converting a ASCII code into string character](#converting-a-ascii-code-into-string-character)
- [finding substring from index a to b](#finding-substring-from-index-a-to-b)
- [finding uppercase of a string](#finding-uppercase-of-a-string)
- [finding lowercase of a string](#finding-lowercase-of-a-string)
- [split a string based on specific string](#split-a-string-based-on-specific-string)
- [trimming a string from left side](#trimming-a-string-from-left-side)
- [trimming a string from right side](#trimming-a-string-from-right-side)
- [trimming a string from both side](#trimming-a-string-from-both-side)
- [checking if string has a specific string](#checking-if-string-has-a-specific-string)
- [replacing a substring with new string](#replacing-a-substring-with-new-string)
- [finding the index of specific string](#finding-the-index-of-specific-string)
- [finding the last index of specific string](#finding-the-last-index-of-specific-string)
- [check if a string starts with a specific string](#check-if-a-string-starts-with-a-specific-string)
- [check if a string ends with a specific string](#check-if-a-string-ends-with-a-specific-string)
- [repeat a string](#repeat-a-string)

## Single line strings

```go
s := "Single line string"
fmt.Println(s)
```

**Output:**

```
Single line string
```

## Multiline strings

```go
s := `This is a
multiline string`
fmt.Println(s)
```

**Output:**

```
This is a
multiline string
```

## Template Literals/String Interpolation

```go
name, age, married := "Raj", 30, false
s := fmt.Sprintf("Name=%s, Age=%d, Married=%t", name, age, married)
fmt.Println(s)
```

**Output:**

```
Name=Raj, Age=30, Married=false
```

## Formatted strings

```go
fmt.Printf("%-8s%-8s%-8s\n", "Name", "Age", "Married")
fmt.Printf("%-8s%-8d%-8t\n", "John", 20, false)
fmt.Printf("%-8s%-8d%-8t\n", "Alex", 24, true)
```

**Output:**

```
Name    Age     Married 
John    20      false   
Alex    24      true
```

## Accessing the character of string at specific index

```go
s := "The quick brown fox jumps over the lazy dog"
fmt.Println(s)
fmt.Printf("1st character: %c\n", s[0])
fmt.Printf("2nd character: %c\n", s[1])
```

**Output:**

```
The quick brown fox jumps over the lazy dog
1st character: T
2nd character: h
```

## Traversing through a string

```go
s := "ABC"
fmt.Println(s)
for i, e := range s {
  fmt.Println(i, string(e))
}
```

**Output:**

```
ABC
0 A
1 B
2 C
```

## Comparing 2 strings

```go
a := "ABC"
b := "DEF"
fmt.Printf("a=%s, b=%s\n", a, b)
if strings.Compare(a, b) == -1 {
  fmt.Println("a comes first")
} else if strings.Compare(a, b) == 1 {
  fmt.Println("b comes first")
} else {
  fmt.Println("a equals b")
}
```

**Output:**

```
a=ABC, b=DEF
a comes first
```

## Getting string size

```go
a := "ABC"
fmt.Printf("a=%s, len(a)=%d\n", a, len(a))
```

**Output:**

```
a=ABC, len(a)=3
```

## Concatenating strings

```go
c := "ABC" + "DEF"
fmt.Println(c)
```

**Output:**

```
ABCDEF
```

## Reversing a string

```go
s := "ABCDEF"
r := ""
for _, ch := range s {
  r = string(ch) + r
}
fmt.Println(r)
```

**Output:**

```
FEDCBA
```

## Converting a string character into ASCII code

```go
s := "ABCDEF"
n := s[0]
fmt.Println(n)
```

**Output:**

```
65
```

## Converting a ASCII code into string character

```go
n := 65
s := fmt.Sprintf("%d", n)
fmt.Println(s)
fmt.Printf("Typeof s: %T\n", s)
```

**Output:**

```
A
Typeof s: string
```

## finding substring from index a to b

```go
s := "Hello World"
fmt.Println(s)
fmt.Println(s[1:5])
```

**Output:**

```
Hello World
ello
```

## finding uppercase of a string

```go
s := "Hello World"
fmt.Println(strings.ToUpper(s))
```

**Output:**

```
HELLO WORLD
```

## finding lowercase of a string

```go
s := "Hello World"
fmt.Println(strings.ToLower(s))
```

**Output:**

```
hello world
```

## split a string based on specific string

```go
s := "Hello World"
list := strings.Split(s, " ")
fmt.Println(list)
```

**Output:**

```
[Hello World]
```

## trimming a string from left side

```go
s := "\n   Hello World"
trimmed := strings.TrimLeft(s, " \n")
fmt.Println(trimmed)
```

**Output:**

```
Hello World
```

## trimming a string from right side

```go
s := "Hello World  \n\n\n"
trimmed := strings.TrimRight(s, " \n")
fmt.Println(trimmed)
```

**Output:**

```
Hello World
```

## trimming a string from both side

```go
s := "\n\n\n   Hello World  \n\n\n"
trimmed := strings.Trim(s, " \n")
fmt.Println(trimmed)
```

**Output:**

```
Hello World
```

## checking if string has a specific string

```go
s := "The quick brown fox jumps over the lazy dog"
fmt.Println(s)
if strings.Contains(s, "lazy") {
  fmt.Println("String contains 'lazy'")
} else {
  fmt.Println("String does not contains 'lazy'")
}
```

**Output:**

```
The quick brown fox jumps over the lazy dog
String contains 'lazy'
```

## replacing a substring with new string

```go
s := "I am Rituraj. mY age is 30, mY country is India"
fmt.Println(s)
fmt.Println(strings.ReplaceAll(s, "mY", "My"))
```

**Output:**

```
I am Rituraj. mY age is 30, mY country is India
I am Rituraj. My age is 30, My country is India
```

## finding the index of specific string

```go
s := "The quick brown fox jumps over the lazy dog"
  fmt.Println(s)
fmt.Println("Index of 'fox':", strings.Index(s, "fox"))
```

**Output:**

```
The quick brown fox jumps over the lazy dog
Index of 'fox': 16
```

## finding the last index of specific string

```go
s := "The quick brown fox jumps over the lazy dog"
fmt.Println(s)
fmt.Println("Last Index of 'o':", strings.LastIndex(s, "o"))
```

**Output:**

```
The quick brown fox jumps over the lazy dog
Last Index of 'o': 41
```

## check if a string starts with a specific string

```go
s := "The quick brown fox jumps over the lazy dog"
fmt.Println(s)
fmt.Println("Starts with 'The':", strings.HasPrefix(s, "The"))
```

**Output:**

```
The quick brown fox jumps over the lazy dog
Starts with 'The': true
```

## check if a string ends with a specific string

```go
s := "The quick brown fox jumps over the lazy dog"
fmt.Println(s)
fmt.Println("Ends with 'dog':", strings.HasSuffix(s, "dog"))
```

**Output:**

```
The quick brown fox jumps over the lazy dog
Ends with 'dog': true
```

## repeat a string

```go
s := "ABC"
fmt.Println(strings.Repeat(s, 3))
```

**Output:**

```
ABCABCABC
```

# Navigations

| [< Previous Page](./console-io.md) | [Home Page](../README.md) | [Next Page >](./data-types.md) |
|---|---|---|
