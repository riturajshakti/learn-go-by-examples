# JSON

| [🏠Goto Home](../README.md) | [Goto Bottom🔻](#navigations) |
|---|---|

# Topics

- [converting a data into json string](#converting-a-data-into-json-string)
- [converting a data into json string with specific indentation](#converting-a-data-into-json-string-with-specific-indentation)
- [converting a typed data into json string](#converting-a-typed-data-into-json-string)
- [converting a json string into typed data](#converting-a-json-string-into-typed-data)
- [converting a json string into data](#converting-a-json-string-into-data)
- [deep clone a data](#deep-clone-a-data)
- [validating json string](#validating-json-string)

## converting a data into json string

```go
data := map[string]any{
  "count":    34,
  "price":    68.34,
  "currency": "usd",
  "isLocal":  false,
}
str, err := json.Marshal(data)
if err != nil {
  fmt.Println(err)
  return
}
fmt.Println(string(str))
```

**Output:**

```
{"count":34,"currency":"usd","isLocal":false,"price":68.34}
```

## converting a data into json string with specific indentation

```go
data := map[string]any{
  "count":    34,
  "price":    68.34,
  "currency": "usd",
  "isLocal":  false,
}
str, err := json.MarshalIndent(data, "", "  ")
if err != nil {
  fmt.Println(err)
  return
}
fmt.Println(string(str))
```

**Output:**

```
{
  "count": 34,
  "currency": "usd",
  "isLocal": false,
  "price": 68.34
}
```

## converting a typed data into json string

```go
type Address struct {
  Line    string `json:"line"`
  Pin     string `json:"pin"`
  City    string `json:"city"`
  Country string `json:"country"`
}

func main() {
  user := User{
    Name:      "Jai",
    Age:       34,
    IsMarried: true,
    Address: Address{
      Line:    "Road No. 25",
      Pin:     "123456",
      City:    "Rock Port",
      Country: "UK",
    },
  }
  str, err := json.MarshalIndent(user, "", "  ")
  if err != nil {
    fmt.Println(err)
    return
  }
  fmt.Println(string(str))
}
```

**Output:**

```
{
  "name": "Jai",
  "age": 34,
  "isMarried": true,
  "address": {
    "line": "Road No. 25",
    "pin": "123456",
    "city": "Rock Port",
    "country": "UK"
  }
}
```

## converting a json string into typed data

```go
type User struct {
  Name      string  `json:"name"`
  Age       int     `json:"age"`
  IsMarried bool    `json:"isMarried"`
  Address   Address `json:"address"`
}

type Address struct {
  Line    string `json:"line"`
  Pin     string `json:"pin"`
  City    string `json:"city"`
  Country string `json:"country"`
}

func main() {
  var user User
  str := `{"name":"Jai","age":34,"isMarried":true,"address":{"line":"Road No. 25","pin":"123456","city":"Rock Port","country":"UK"}}`
  err := json.Unmarshal([]byte(str), &user)
  if err != nil {
    fmt.Println(err)
    return
  }
  fmt.Println(user)
}
```

**Output:**

```
{Jai 34 true {Road No. 25 123456 Rock Port UK}}
```

## converting a json string into data

```go
package main

import (
  "encoding/json"
  "fmt"
)

func main() {
  var user map[string]any
  str := `{"name":"Jai","age":34,"isMarried":true,"address":{"line":"Road No. 25","pin":"123456","city":"Rock Port","country":"UK"}}`
  err := json.Unmarshal([]byte(str), &user)
  if err != nil {
    fmt.Println(err)
    return
  }
  fmt.Println(user)
}
```

**Output:**

```
map[address:map[city:Rock Port country:UK line:Road No. 25 pin:123456] age:34 isMarried:true name:Jai]
```

## deep clone a data

```go
data := map[string]any{
  "count":    34,
  "price":    68.34,
  "currency": "usd",
  "isLocal":  false,
}
str, _ := json.Marshal(data)
var cloned map[string]any
json.Unmarshal(str, &cloned)
fmt.Println(cloned)
```

**Output:**

```
map[count:34 currency:usd isLocal:false price:68.34]
```

## validating json string

```go
var temp any
str := `{"count":34,"currency":"usd","isLocal":false,"price":68.34}`
err := json.Unmarshal([]byte(str), &temp)
if err == nil {
  fmt.Println("JSON string is valid")
} else {
  fmt.Println("JSON string is invalid")
}
```

**Output:**

```
JSON string is valid
```

# Navigations

| [< Previous Page](./functions.md) | [Home Page](../README.md) | [Next Page >](./errors.md) |
|---|---|---|
