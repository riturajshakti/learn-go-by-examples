[Goto Home](../README.md)

# Creating a struct

```go
type User struct {
  Name string
  Age  int
}

func main() {
  user1 := User{"John", 23}
  fmt.Println(user1)

  user2 := User{Name: "Alex", Age: 20}
  fmt.Println(user2)
}
```

**Output:**

```
{John 23}
{Alex 20}
```

# Creating Anonymous Struct

```go
user := struct {
  Name string
  Age  int
}{"John", 23}
fmt.Println(user)

car := struct {
  Model string
  Color string
}{
  Model: "Tesla",
  Color: "red",
}
fmt.Println(car)
```

**Output:**

```
{John 23}
{Tesla red}
```

# checking if a property exist in an object

```go
type User struct {
  Name string
  Age  int
}

func main() {
  user := User{"John", 23}
  fmt.Println(user)

  fieldName := "Age"
  _, ok := reflect.TypeOf(user).FieldByName(fieldName)
  if ok {
    fmt.Println(fieldName, "exist in User struct")
  } else {
    fmt.Println(fieldName, "doesn't exist in User struct")
  }
}
```

**Output:**

```
{John 23}
Age exist in User struct
```

# Traversing through all properties and its details in a struct

```go
type User struct {
  Name string `json:"name" xml:"NAME"`
  Age  int    `json:"age" xml:"AGE"`
}

func main() {
  user := User{"John", 23}
  fmt.Println(user)

  userType := reflect.TypeOf(user)
  for i := range userType.NumField() {
    field := userType.Field(i)
    fmt.Println("Field name:", field.Name)
    fmt.Println("Field type:", field.Type)
    fmt.Println("Field Tag:", field.Tag)
    fmt.Println("Field Tag (json):", field.Tag.Get("json"))
    fmt.Println("Field Tag (xml):", field.Tag.Get("xml"))
    fmt.Println("---------")
  }
}
```

**Output:**

```
{John 23}
Field name: Name
Field type: string
Field Tag: json:"name" xml:"NAME"
Field Tag (json): name
Field Tag (xml): NAME
---------
Field name: Age
Field type: int
Field Tag: json:"age" xml:"AGE"
Field Tag (json): age
Field Tag (xml): AGE
---------
```

# instance methods

```go
type User struct {
  Name string
  Age  int
}

func (user User) String() string {
  return fmt.Sprintf("User{Name: %s, Age: %d}", user.Name, user.Age)
}

func main() {
  user := User{"John", 23}
  fmt.Println(user.String())
  fmt.Println(user)
}
```

**Output:**

```
User{Name: John, Age: 23}
User{Name: John, Age: 23}
```

# Composition

```go
type User struct {
  Name    string
  Age     int
  Address Address
}

type Address struct {
  Line    string
  City    string
  Pin     string
  Country string
}

func main() {
  user := User{"John", 23, Address{"B 123, Rd 23", "Rock Port", "123456", "UK"}}
  fmt.Println(user)
}
```

**Output:**

```
{John 23 {B 123, Rd 23 Rock Port 123456 UK}}
```
