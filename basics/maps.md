# Maps

| [🏠Goto Home](../README.md) | [Goto Bottom🔻](#navigations) |
|---|---|

# Topics

- [Creating an empty map](#creating-an-empty-map)
- [Setting key-value pair on a map](#setting-key-value-pair-on-a-map)
- [Checking if a key exist in a map](#checking-if-a-key-exist-in-a-map)
- [Accessing value on specific key of map](#accessing-value-on-specific-key-of-map)
- [Updating value on specific key of map](#updating-value-on-specific-key-of-map)
- [Deleting a key-value pair from a map](#deleting-a-key-value-pair-from-a-map)
- [Clearing the map](#clearing-the-map)
- [Getting map size](#getting-map-size)
- [Getting keys list of a map](#getting-keys-list-of-a-map)
- [Getting values list of a map](#getting-values-list-of-a-map)
- [Traversing a map](#traversing-a-map)
- [Merging 2 maps into one](#merging-2-maps-into-one)

## Creating an empty map

```go
m := map[string]any{}
fmt.Println(m)
```

**Output:**

```
map[]
```

## Setting key-value pair on a map

```go
m := map[string]any{}
m["name"] = "John"
m["age"] = 45
fmt.Println(m)
```

**Output:**

```
map[age:45 name:John]
```

## Checking if a key exist in a map

```go
m := map[string]any{"name": "John", "age": 34}
if _, exist := m["name"]; exist {
  fmt.Println("name key exist in the map")
} else {
  fmt.Println("name key does not exist in the map")
}
```

**Output:**

```
name key exist in the map
```

## Accessing value on specific key of map

```go
m := map[string]any{"name": "John", "age": 34}
fmt.Println(m["name"])
fmt.Println(m["age"])
```

**Output:**

```
John
34
```

## Updating value on specific key of map

```go
m := map[string]any{"name": "John", "age": 34}
m["name"] = "Raj"
fmt.Println(m)
```

**Output:**

```
map[age:34 name:Raj]
```

## Deleting a key-value pair from a map

```go
m := map[string]any{"name": "John", "age": 34}
delete(m, "name")
fmt.Println(m)
```

**Output:**

```
map[age:34]
```

## Clearing the map

```go
m := map[string]any{"name": "John", "age": 34}
clear(m)
fmt.Println(m)
```

**Output:**

```
map[]
```

## Getting map size

```go
m := map[string]any{"name": "John", "age": 34}
fmt.Println(len(m))
```

**Output:**

```
2
```

## Getting keys list of a map

```go
m := map[string]any{"name": "John", "age": 34}
keys := []string{}
for k := range m {
  keys = append(keys, k)
}
fmt.Println(keys)
```

**Output:**

```
[name age]
```

## Getting values list of a map

```go
m := map[string]any{"name": "John", "age": 34}
values := []any{}
for _, v := range m {
  values = append(values, v)
}
fmt.Println(values)
```

**Output:**

```
[John 34]
```

## Traversing a map

```go
m := map[string]any{"name": "John", "age": 34}
for k, v := range m {
  fmt.Println(k, v)
}
```

**Output:**

```
name John
age 34
```

## Merging 2 maps into one

```go
m := map[string]any{"name": "John", "age": 34}
n := map[string]any{"married": true}
mixed := map[string]any{}
maps.Copy(mixed, m)
maps.Copy(mixed, n)
fmt.Println(mixed)
```

**Output:**

```
map[age:34 married:true name:John]
```

# Navigations

| [< Previous Page](./slices.md) | [Home Page](../README.md) | [Next Page >](./regex.md) |
|---|---|---|
