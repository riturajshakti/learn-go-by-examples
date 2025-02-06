[Goto Home](../README.md)

# Basic GET api call which returns regular JSON

**1st Method:** using http.Get

```go
package main

import (
  "fmt"
  "io"
  "net/http"
)

func main() {
  url := "https://jsonplaceholder.typicode.com/posts/1"
  res, err := http.Get(url)
  if err != nil {
    fmt.Println(err)
    return
  }
  defer res.Body.Close()

  if res.StatusCode != http.StatusOK {
    fmt.Println("Request failed with status:", res.Status)
    return
  }

  jsonString, err := io.ReadAll(res.Body)
  if err != nil {
    fmt.Println(err)
    return
  }

  fmt.Println(string(jsonString))
}
```

**Output:**

```
{
  "userId": 1,
  "id": 1,
  "title": "sunt aut facere repellat provident occaecati excepturi optio reprehenderit",
  "body": "quia et suscipit\nsuscipit recusandae consequuntur expedita et cum\nreprehenderit molestiae ut ut quas totam\nnostrum rerum est autem sunt rem eveniet architecto"        
}
```

**2nd Method:** Using http.NewRequest for more control

```go
package main

import (
  "fmt"
  "io"
  "net/http"
  "time"
)

func main() {
  url := "https://jsonplaceholder.typicode.com/posts/1"
  client := &http.Client{Timeout: 10 * time.Second}
  req, err := http.NewRequest("GET", url, nil)
  if err != nil {
    fmt.Println(err)
    return
  }

  res, err := client.Do(req)
  if err != nil {
    fmt.Println(err)
    return
  }
  defer res.Body.Close()

  if res.StatusCode != http.StatusOK {
    fmt.Println("Request failed with status:", res.Status)
    return
  }

  jsonString, err := io.ReadAll(res.Body)
  if err != nil {
    fmt.Println(err)
    return
  }

  fmt.Println(string(jsonString))
}
```

**Output:**

```
{
  "userId": 1,
  "id": 1,
  "title": "sunt aut facere repellat provident occaecati excepturi optio reprehenderit",
  "body": "quia et suscipit\nsuscipit recusandae consequuntur expedita et cum\nreprehenderit molestiae ut ut quas totam\nnostrum rerum est autem sunt rem eveniet architecto"        
}
```

**3rd Method:** Using `github.com/riturajshakti/apicall` package for simplicity

```go
package main

import (
  "fmt"

  "github.com/riturajshakti/apicall"
)

func main() {
  res, err := apicall.ApiCall(&apicall.Request{
    Url: "https://jsonplaceholder.typicode.com/posts/1",
  })
  if err != nil {
    fmt.Println(err)
    return
  }

  if res.StatusCode != 200 {
    fmt.Println("API call was not successful:", res.StatusMessage)
    return
  }

  fmt.Println("Status Code:", res.StatusCode)
  fmt.Println("Status Message:", res.StatusMessage)
  fmt.Println("Json:", res.Json)
  fmt.Println("Body:", string(res.Body))
}
```

**Output:**

```
Status Code: 200
Status Message: OK
Json: map[body:quia et suscipit
suscipit recusandae consequuntur expedita et cum
reprehenderit molestiae ut ut quas totam
nostrum rerum est autem sunt rem eveniet architecto id:1 title:sunt aut facere repellat provident occaecati excepturi optio reprehenderit userId:1]
Body: {
  "userId": 1,
  "id": 1,
  "title": "sunt aut facere repellat provident occaecati excepturi optio reprehenderit",
  "body": "quia et suscipit\nsuscipit recusandae consequuntur expedita et cum\nreprehenderit molestiae ut ut quas totam\nnostrum rerum est autem sunt rem eveniet architecto"        
}
```

# POST/PUT/PATCH/DELETE api call with json payload

**1st Method:** Using http.Post

```go
package main

import (
  "bytes"
  "encoding/json"
  "fmt"
  "io"
  "net/http"
)

type Post struct {
  Title  string `json:"title"`
  Body   string `json:"body"`
  UserID int    `json:"userId"`
}

func main() {
  postData := Post{
    Title:  "New Post",
    Body:   "This is a test post",
    UserID: 1,
  }

  jsonData, err := json.Marshal(postData)
  if err != nil {
    fmt.Println(err)
    return
  }

  url := "https://jsonplaceholder.typicode.com/posts"
  res, err := http.Post(url, "application/json", bytes.NewBuffer(jsonData))
  if err != nil {
    fmt.Println(err)
    return
  }
  defer res.Body.Close()

  if res.StatusCode != http.StatusCreated {
    fmt.Println("Request failed with status:", res.Status)
    return
  }

  jsonString, err := io.ReadAll(res.Body)
  if err != nil {
    fmt.Println(err)
    return
  }

  fmt.Println(string(jsonString))
}
```

**Output:**

```
{
  "title": "New Post",
  "body": "This is a test post",
  "userId": 1,
  "id": 101
}
```

**2nd Method:** using http.NewRequest for more control

```go
package main

import (
  "bytes"
  "encoding/json"
  "fmt"
  "io"
  "net/http"
  "time"
)

type Post struct {
  Title  string `json:"title"`
  Body   string `json:"body"`
  UserID int    `json:"userId"`
}

func main() {
  url := "https://jsonplaceholder.typicode.com/posts"

  postData := Post{
    Title:  "Advanced Post",
    Body:   "This is an advanced test post",
    UserID: 1,
  }

  jsonData, err := json.Marshal(postData)
  if err != nil {
    fmt.Println(err)
    return
  }

  client := &http.Client{Timeout: 10 * time.Second}
  req, err := http.NewRequest("POST", url, bytes.NewBuffer(jsonData))
  if err != nil {
    fmt.Println("Error creating request:", err)
    return
  }

  req.Header.Set("Content-Type", "application/json")

  resp, err := client.Do(req)
  if err != nil {
    fmt.Println(err)
    return
  }
  defer resp.Body.Close()

  body, err := io.ReadAll(resp.Body)
  if err != nil {
    fmt.Println(err)
    return
  }

  fmt.Println(string(body))
}
```

**Output:**

```
{
  "title": "Advanced Post",
  "body": "This is an advanced test post",
  "userId": 1,
  "id": 101
}
```

**3rd Method:** Using `github.com/riturajshakti/apicall` package for simplicity

```go
package main

import (
  "fmt"
  "time"

  "github.com/riturajshakti/apicall"
)

type Post struct {
  Title  string `json:"title"`
  Body   string `json:"body"`
  UserID int    `json:"userId"`
}

func main() {
  postData := Post{
    Title:  "Advanced Post",
    Body:   "This is an advanced test post",
    UserID: 1,
  }

  res, err := apicall.ApiCall(&apicall.Request{
    Url:     "https://jsonplaceholder.typicode.com/posts",
    Json:    postData,
    Method:  apicall.POST,
    Timeout: 10 * time.Second,
  })
  if err != nil {
    fmt.Println(err)
    return
  }

  if res.StatusCode != 201 {
    fmt.Println("API call was not successful:", res.StatusMessage)
    return
  }

  fmt.Println("Json:", res.Json)
  fmt.Println("Body:", string(res.Body))
}
```

**Output:**

```
Json: map[body:This is an advanced test post id:101 title:Advanced Post userId:1]
Body: {
  "title": "Advanced Post",
  "body": "This is an advanced test post",
  "userId": 1,
  "id": 101
}
```

# Form data upload with files and string fields

**1st Method:** Using http.Post

```go
package main

import (
  "bytes"
  "fmt"
  "io"
  "mime/multipart"
  "net/http"
  "os"
)

func main() {
  filePath := "file.txt"

  var requestBody bytes.Buffer
  writer := multipart.NewWriter(&requestBody)

  _ = writer.WriteField("name", "john")
  _ = writer.WriteField("age", "20")

  file, err := os.Open(filePath)
  if err != nil {
    fmt.Println("Error opening file:", err)
    return
  }
  defer file.Close()

  part, err := writer.CreateFormFile("file", filePath)
  if err != nil {
    fmt.Println("Error creating form file:", err)
    return
  }

  _, err = io.Copy(part, file)
  if err != nil {
    fmt.Println("Error copying file content:", err)
    return
  }

  writer.Close()

  res, err := http.Post(
    "https://api.escuelajs.co/api/v1/files/upload",
    writer.FormDataContentType(),
    &requestBody,
  )
  if err != nil {
    fmt.Println("Error sending request:", err)
    return
  }
  defer res.Body.Close()

  responseBody, err := io.ReadAll(res.Body)
  if err != nil {
    fmt.Println("Error reading response body:", err)
    return
  }

  fmt.Println("Response Status:", res.Status)
  fmt.Println("Response Body:", string(responseBody))
}
```

**Output:**

```
Response Status: 201 Created
Response Body: {"originalname":"file.txt","filename":"d6f2.txt","location":"https://api.escuelajs.co/api/v1/files/d6f2.txt"}
```

**2nd Method:** Using http.NewRequest for more control

```go
package main

import (
  "bytes"
  "fmt"
  "io"
  "mime/multipart"
  "net/http"
  "os"
)

func main() {
  filePath := "file.txt"

  var requestBody bytes.Buffer
  writer := multipart.NewWriter(&requestBody)

  err := writer.WriteField("name", "john")
  if err != nil {
    fmt.Println("Error writing name field:", err)
    return
  }

  err = writer.WriteField("age", "20")
  if err != nil {
    fmt.Println("Error writing age field:", err)
    return
  }

  file, err := os.Open(filePath)
  if err != nil {
    fmt.Println("Error opening file:", err)
    return
  }
  defer file.Close()

  part, err := writer.CreateFormFile("file", filePath)
  if err != nil {
    fmt.Println("Error creating form file:", err)
    return
  }

  _, err = io.Copy(part, file)
  if err != nil {
    fmt.Println("Error copying file content:", err)
    return
  }

  writer.Close()
  req, err := http.NewRequest("POST", "https://api.escuelajs.co/api/v1/files/upload", &requestBody)
  if err != nil {
    fmt.Println("Error creating request:", err)
    return
  }

  req.Header.Set("Content-Type", writer.FormDataContentType())

  client := &http.Client{}
  res, err := client.Do(req)
  if err != nil {
    fmt.Println("Error sending request:", err)
    return
  }
  defer res.Body.Close()

  if res.StatusCode != 201 {
    fmt.Println("Error:", res.Status)
    return
  }

  responseBody, err := io.ReadAll(res.Body)
  if err != nil {
    fmt.Println("Error reading response body:", err)
    return
  }

  fmt.Println("Response Status:", res.Status)
  fmt.Println("Response Body:", string(responseBody))
}
```

**Output:**

```
Response Status: 201 Created
Response Body: {"originalname":"file.txt","filename":"10622.txt","location":"https://api.escuelajs.co/api/v1/files/10622.txt"}
```

**3rd Method:** using `github.com/riturajshakti/apicall` for simplicity

```go
package main

import (
  "fmt"

  "github.com/riturajshakti/apicall"
)

func main() {
  res, err := apicall.ApiCall(&apicall.Request{
    Url:    "https://api.escuelajs.co/api/v1/files/upload",
    Method: "POST",
    FormData: &apicall.FormData{
      Files: map[string]any{
        "file": "file.txt",
        // "songs": []string{"music1.mp3", "music2.mp3"},
      },
      Fields: map[string]string{
        "name": "John",
        "age":  "20",
      },
    },
  })

  if err != nil {
    fmt.Println(err)
    return
  }

  if !res.Ok {
    fmt.Println(res.StatusMessage)
    return
  }

  fmt.Println(res.Json)
}
```

**Output:**

```
map[filename:32106.txt location:https://api.escuelajs.co/api/v1/files/32106.txt originalname:file.txt]
```

# Print file upload percentage

**1st Method:** Using custom go code

```go
package main

import (
  "bytes"
  "fmt"
  "io"
  "mime/multipart"
  "net/http"
  "os"
)

type ProgressReader struct {
  io.Reader
  Total    int64
  Uploaded int64
}

func (p *ProgressReader) Read(buf []byte) (int, error) {
  n, err := p.Reader.Read(buf)
  if n > 0 {
    p.Uploaded += int64(n)
    percentage := (float64(p.Uploaded) / float64(p.Total)) * 100
    fmt.Printf("\rUploading: %.2f%%", percentage)
  }
  return n, err
}

func main() {
  filePath := "file.txt"

  var requestBody bytes.Buffer
  writer := multipart.NewWriter(&requestBody)

  _ = writer.WriteField("name", "john")
  _ = writer.WriteField("age", "20")

  file, err := os.Open(filePath)
  if err != nil {
    fmt.Println("Error opening file:", err)
    return
  }
  defer file.Close()

  part, err := writer.CreateFormFile("file", filePath)
  if err != nil {
    fmt.Println("Error creating form file:", err)
    return
  }

  _, err = io.Copy(part, file)
  if err != nil {
    fmt.Println("Error copying file content:", err)
    return
  }

  writer.Close()

  progressReader := &ProgressReader{
    Reader: bytes.NewReader(requestBody.Bytes()),
    Total:  int64(requestBody.Len()),
  }

  req, err := http.NewRequest("POST", "https://api.escuelajs.co/api/v1/files/upload", progressReader)
  if err != nil {
    fmt.Println("Error creating request:", err)
    return
  }

  req.Header.Set("Content-Type", writer.FormDataContentType())

  client := &http.Client{}
  res, err := client.Do(req)
  if err != nil {
    fmt.Println("Error sending request:", err)
    return
  }
  defer res.Body.Close()

  fmt.Println("\nUpload complete!")

  responseBody, err := io.ReadAll(res.Body)
  if err != nil {
    fmt.Println("Error reading response body:", err)
    return
  }

  fmt.Println("Response Status:", res.Status)
  fmt.Println("Response Body:", string(responseBody))
}
```

**Output:**

```
Uploading: 100.00%
Upload complete!
Response Status: 201 Created
Response Body: {"originalname":"file.txt","filename":"97ed.txt","location":"https://api.escuelajs.co/api/v1/files/97ed.txt"}
```

**2nd Method:** using `github.com/riturajshakti/apicall` for simplicity

```go
package main

import (
  "fmt"

  "github.com/riturajshakti/apicall"
)

func main() {
  res, err := apicall.ApiCall(&apicall.Request{
    Url:    "https://api.escuelajs.co/api/v1/files/upload",
    Method: "POST",
    FormData: &apicall.FormData{
      Files: map[string]any{
        "file": "file.txt",
      },
      Fields: map[string]string{
        "name": "John",
        "age":  "20",
      },
    },
    OnProgress: func(uploaded int64, total int64) {
      percentage := (float64(uploaded) / float64(total)) * 100
      fmt.Printf("\rUploading: %.2f%%", percentage)
      if uploaded == total {
        fmt.Println("\nUpload complete!")
      }
    },
  })

  if err != nil {
    fmt.Println(err)
    return
  }

  if !res.Ok {
    fmt.Println(res.StatusMessage)
    return
  }

  fmt.Println(res.Json)
}
```

**Output:**

```
Uploading: 100.00%
Upload complete!
map[filename:2f13.txt location:https://api.escuelajs.co/api/v1/files/2f13.txt originalname:file.txt]
```

# Set Headers in request payload

**1st Method:** Using custom go code

```go
package main

import (
  "bytes"
  "encoding/json"
  "fmt"
  "io"
  "net/http"
  "time"
)

type Post struct {
  Title  string `json:"title"`
  Body   string `json:"body"`
  UserID int    `json:"userId"`
}

func main() {
  url := "https://jsonplaceholder.typicode.com/posts"

  postData := Post{
    Title:  "Advanced Post",
    Body:   "This is an advanced test post",
    UserID: 1,
  }

  jsonData, err := json.Marshal(postData)
  if err != nil {
    fmt.Println(err)
    return
  }

  client := &http.Client{Timeout: 10 * time.Second}
  req, err := http.NewRequest("POST", url, bytes.NewBuffer(jsonData))
  if err != nil {
    fmt.Println("Error creating request:", err)
    return
  }

  req.Header.Set("Content-Type", "application/json")

  resp, err := client.Do(req)
  if err != nil {
    fmt.Println(err)
    return
  }
  defer resp.Body.Close()

  body, err := io.ReadAll(resp.Body)
  if err != nil {
    fmt.Println(err)
    return
  }

  fmt.Println(string(body))
}
```

**Output:**

```
{
  "title": "Advanced Post",
  "body": "This is an advanced test post",
  "userId": 1,
  "id": 101
}
```

**2nd Method:** Setting headers when using `github.com/riturajshakti/apicall`

```go
package main

import (
  "encoding/json"
  "fmt"

  "github.com/riturajshakti/apicall"
)

type Post struct {
  Title  string `json:"title"`
  Body   string `json:"body"`
  UserID int    `json:"userId"`
}

func main() {
  postData := Post{
    Title:  "Advanced Post",
    Body:   "This is an advanced test post",
    UserID: 1,
  }

  jsonString, _ := json.Marshal(postData)

  res, err := apicall.ApiCall(&apicall.Request{
    Url:    "https://jsonplaceholder.typicode.com/posts",
    Method: apicall.POST,
    Headers: map[string]string{
      "Content-Type": "application/json",
    },
    Body: jsonString,
  })
  if err != nil {
    fmt.Println(err)
    return
  }

  if res.StatusCode != 201 {
    fmt.Println("API call was not successful:", res.StatusMessage)
    return
  }

  fmt.Println("Json:", res.Json)
}
```

**Output:**

```
Json: map[body:This is an advanced test post id:101 title:Advanced Post userId:1]
```

# Set URL Search Params in request payload

**1st Method:** Using http.Get

```go
package main

import (
  "fmt"
  "io"
  "net/http"
  "net/url"
)

func main() {
  baseURL := "https://jsonplaceholder.typicode.com/posts"

  parsedURL, err := url.Parse(baseURL)
  if err != nil {
    fmt.Println("Error parsing URL:", err)
    return
  }

  query := parsedURL.Query()
  query.Set("limit", "5")
  query.Set("page", "2")
  parsedURL.RawQuery = query.Encode()

  res, err := http.Get(parsedURL.String())
  if err != nil {
    fmt.Println("Error sending request:", err)
    return
  }
  defer res.Body.Close()

  if res.StatusCode != http.StatusOK {
    fmt.Println("Request failed with status:", res.Status)
    return
  }

  jsonString, err := io.ReadAll(res.Body)
  if err != nil {
    fmt.Println("Error reading response:", err)
    return
  }

  fmt.Println(string(jsonString))
}
```

**Output:**

```json
[
  {
    "userId": 1,
    "id": 6,
    "title": "dolorem eum magni eos aperiam quia",
    "body": "ut aspernatur corporis harum nihil quis provident sequi\nmollitia nobis aliquid molestiae\nperspiciatis et ea nemo ab reprehenderit accusantium quas\nvoluptate dolores 
velit et doloremque molestiae"
  },
  {
    "userId": 1,
    "id": 7,
    "title": "magnam facilis autem",
    "body": "dolore placeat quibusdam ea quo vitae\nmagni quis enim qui quis quo nemo aut saepe\nquidem repellat excepturi ut quia\nsunt ut sequi eos ea sed quas"
  },
  {
    "userId": 1,
    "id": 8,
    "title": "dolorem dolore est ipsam",
    "body": "dignissimos aperiam dolorem qui eum\nfacilis quibusdam animi sint suscipit qui sint possimus cum\nquaerat magni maiores excepturi\nipsam ut commodi dolor voluptatum modi aut vitae"
  },
  {
    "userId": 1,
    "id": 9,
    "title": "nesciunt iure omnis dolorem tempora et accusantium",
    "body": "consectetur animi nesciunt iure dolore\nenim quia ad\nveniam autem ut quam aut nobis\net est aut quod aut provident voluptas autem voluptas"
  },
  {
    "userId": 1,
    "id": 10,
    "title": "optio molestias id quia eum",
    "body": "quo et expedita modi cum officia vel magni\ndoloribus qui repudiandae\nvero nisi sit\nquos veniam quod sed accusamus veritatis error"
  }
]
```

**2nd Method:** Using `github.com/riturajshakti/apicall` package for simplicity

```go
package main

import (
  "fmt"

  "github.com/riturajshakti/apicall"
)

func main() {
  res, err := apicall.ApiCall(&apicall.Request{
    Url: "https://jsonplaceholder.typicode.com/posts/1",
    Query: map[string]string{
      "limit": "10",
      "page":  "2",
    },
  })
  if err != nil {
    fmt.Println(err)
    return
  }

  if res.StatusCode != 200 {
    fmt.Println("API call was not successful:", res.StatusMessage)
    return
  }

  fmt.Println("Status Code:", res.StatusCode)
  fmt.Println("Status Message:", res.StatusMessage)
  fmt.Println("Json:", string(res.Body))
}
```

**Output:**

```
Status Code: 200
Status Message: OK
Json: {
  "userId": 1,
  "id": 1,
  "title": "sunt aut facere repellat provident occaecati excepturi optio reprehenderit",
  "body": "quia et suscipit\nsuscipit recusandae consequuntur expedita et cum\nreprehenderit molestiae ut ut quas totam\nnostrum rerum est autem sunt rem eveniet architecto"        
}
```

# Accessing Response Data

**1st Method:** Using custom go code

```go
package main

import (
  "fmt"
  "io"
  "net/http"
)

func main() {
  url := "https://jsonplaceholder.typicode.com/posts/1"
  res, err := http.Get(url)
  if err != nil {
    fmt.Println(err)
    return
  }
  defer res.Body.Close()

  if res.StatusCode != http.StatusOK {
    fmt.Println("Request failed with status:", res.Status)
    return
  }

  jsonString, err := io.ReadAll(res.Body)
  if err != nil {
    fmt.Println(err)
    return
  }

  fmt.Println("Status Code:", res.StatusCode)
  fmt.Println("Status Message:", res.Status)
  fmt.Println("Headers:", res.Header)
  fmt.Println(string(jsonString))
}
```

**Output:**

```
Status Code: 200
Status Message: 200 OK
Headers: map[Access-Control-Allow-Credentials:[true] Age:[26585] Alt-Svc:[h3=":443"; ma=86400] Cache-Control:[max-age=43200] Cf-Cache-Status:[HIT] Cf-Ray:[90d8b19d0dc070ed-MRS] Content-Type:[application/json; charset=utf-8] Date:[Thu, 06 Feb 2025 05:20:55 GMT] Etag:[W/"124-yiKdLzqO5gfBrJFrcdJ8Yq0LGnU"] Expires:[-1] Nel:[{"report_to":"heroku-nel","max_age":3600,"success_fraction":0.005,"failure_fraction":0.05,"response_headers":["Via"]}] Pragma:[no-cache] Report-To:[{"group":"heroku-nel","max_age":3600,"endpoints":[{"url":"https://nel.heroku.com/reports?ts=1738187858&sid=e11707d5-02a7-43ef-b45e-2cf4d2036f7d&s=%2FOGkjgtY0h%2FcXU%2BlXKfrln97yGINMYADUsEbBPfjUm8%3D"}]}] Reporting-Endpoints:[heroku-nel=https://nel.heroku.com/reports?ts=1738187858&sid=e11707d5-02a7-43ef-b45e-2cf4d2036f7d&s=%2FOGkjgtY0h%2FcXU%2BlXKfrln97yGINMYADUsEbBPfjUm8%3D] Server:[cloudflare] Server-Timing:[cfL4;desc="?proto=TCP&rtt=0&min_rtt=4294967295&rtt_var=750000&sent=9&recv=9&lost=0&retrans=2&sent_bytes=4711&recv_bytes=1741&delivery_rate=0&cwnd=234&unsent_bytes=0&cid=4ac475bf5876fbca&ts=2190&x=0"] Vary:[Origin, Accept-Encoding] Via:[1.1 vegur] X-Content-Type-Options:[nosniff] X-Powered-By:[Express] X-Ratelimit-Limit:[1000] X-Ratelimit-Remaining:[999] X-Ratelimit-Reset:[1738187866]]
6]]
{
  "userId": 1,
  "id": 1,
  "title": "sunt aut facere repellat provident occaecati excepturi optio reprehenderit",
  "body": "quia et suscipit\nsuscipit recusandae consequuntur expedita et cum\nreprehenderit molestiae ut ut quas totam\nnostrum rerum est autem sunt rem eveniet architecto"        
}
```

**2nd Method:** Using `github.com/riturajshakti/apicall` package

```go
package main

import (
  "fmt"

  "github.com/riturajshakti/apicall"
)

func main() {
  res, err := apicall.ApiCall(&apicall.Request{
    Url: "https://jsonplaceholder.typicode.com/posts/1",
  })
  if err != nil {
    fmt.Println(err)
    return
  }

  if !res.Ok {
    fmt.Println("API call was not successful:", res.StatusMessage)
    return
  }

  fmt.Println("Ok:", res.Ok)
  fmt.Println("Status Code:", res.StatusCode)
  fmt.Println("Status Message:", res.StatusMessage)
  fmt.Println("Headers:", res.Headers)
  fmt.Println("Json:", res.Json)
  fmt.Println("Body:", string(res.Body))
}
```

**Output:**

```
Ok: true
Status Code: 200
Status Message: OK
Headers: map[Access-Control-Allow-Credentials:true Age:26720 Alt-Svc:h3=":443"; ma=86400 Cache-Control:max-age=43200 Cf-Cache-Status:HIT Cf-Ray:90d8b4eb18e070ed-MRS Content-Type:application/json; charset=utf-8 Date:Thu, 06 Feb 2025 05:23:11 GMT Etag:W/"124-yiKdLzqO5gfBrJFrcdJ8Yq0LGnU" Expires:-1 Nel:{"report_to":"heroku-nel","max_age":3600,"success_fraction":0.005,"failure_fraction":0.05,"response_headers":["Via"]} Pragma:no-cache Report-To:{"group":"heroku-nel","max_age":3600,"endpoints":[{"url":"https://nel.heroku.com/reports?ts=1738187858&sid=e11707d5-02a7-43ef-b45e-2cf4d2036f7d&s=%2FOGkjgtY0h%2FcXU%2BlXKfrln97yGINMYADUsEbBPfjUm8%3D"}]} Reporting-Endpoints:heroku-nel=https://nel.heroku.com/reports?ts=1738187858&sid=e11707d5-02a7-43ef-b45e-2cf4d2036f7d&s=%2FOGkjgtY0h%2FcXU%2BlXKfrln97yGINMYADUsEbBPfjUm8%3D Server:cloudflare Server-Timing:cfL4;desc="?proto=TCP&rtt=131893&min_rtt=131893&rtt_var=65946&sent=12&recv=9&lost=0&retrans=1&sent_bytes=4709&recv_bytes=1741&delivery_rate=18205&cwnd=232&unsent_bytes=0&cid=403000a693e1833b&ts=332&x=0" Vary:Origin, Accept-Encoding Via:1.1 vegur X-Content-Type-Options:nosniff X-Powered-By:Express X-Ratelimit-Limit:1000 X-Ratelimit-Remaining:999 X-Ratelimit-Reset:1738187866]
Json: map[body:quia et suscipit
suscipit recusandae consequuntur expedita et cum
reprehenderit molestiae ut ut quas totam
nostrum rerum est autem sunt rem eveniet architecto id:1 title:sunt aut facere repellat provident occaecati excepturi optio reprehenderit userId:1]
Body: {
  "userId": 1,
  "id": 1,
  "title": "sunt aut facere repellat provident occaecati excepturi optio reprehenderit",
  "body": "quia et suscipit\nsuscipit recusandae consequuntur expedita et cum\nreprehenderit molestiae ut ut quas totam\nnostrum rerum est autem sunt rem eveniet architecto"        
}
```

# Implementing Client Side SSE (Server Sent Events)

**1st Method:** Using bufio.Scanner

```go
package main

import (
  "bufio"
  "fmt"
  "net/http"
  "os"
)

func main() {
  url := "https://sse-fake.andros.dev/events/"

  resp, err := http.Get(url)
  if err != nil {
    fmt.Println("Error connecting to SSE:", err)
    return
  }
  defer resp.Body.Close()

  if resp.StatusCode != http.StatusOK {
    fmt.Println("Unexpected response status:", resp.Status)
    return
  }

  fmt.Println("Connected to SSE stream...")

  // Create a buffered scanner to read the SSE stream line by line
  scanner := bufio.NewScanner(resp.Body)
  for scanner.Scan() {
    line := scanner.Text()

    // Ignore empty lines (SSE events can be multi-line)
    if line == "" {
      continue
    }

    fmt.Println("Event:", line)

    if line == "exit" {
      fmt.Println("Exiting SSE listener...")
      break
    }
  }

  if err := scanner.Err(); err != nil {
    fmt.Println("Error reading SSE stream:", err)
    os.Exit(1)
  }
}
```

**Output:**

```
Connected to SSE stream...
Event: :

Event: event: stream-open
Event: data:
Event: event: message
Event: data: {"action": "New message", "name": "Candace", "text": "Protect newspaper turn front. Part consider wrong be newspaper.\nStand on strategy six safe bar character. Owner color produce beyond read simple staff."}
Event: event: message
Event: data: {"action": "New message", "name": "Vincent", "text": "Relate study same we. Animal number keep every account late. Power rather feel citizen impact."}
Event: event: message
Event: data: {"action": "New message", "name": "Denise", "text": "Car include little agree land member beautiful he.\nRequire writer example everybody themselves chance. Fund push with close whatever card ball.\nAffect staff former fund gas."}
Event: event: message
Event: data: {"action": "New message", "name": "Antonio", "text": "Remember price similar chance music surface green. Long voice economic human real we more explain. Pass sense man 
compare station show final."}
Event: event: message
Event: data: {"action": "User connected", "name": "Sarah"}
Event: event: message
Event: data: {"action": "New message", "name": "Christopher", "text": "Television example attack daughter plant feeling system. Understand if cover dark store fire man course.\nHope across reason eat serve improve. Interview item choice sit.\nBe represent statement pass."}
...
```

**2nd Method:** using reader.ReadString

```go
package main

import (
  "bufio"
  "fmt"
  "net/http"
  "strings"
)

func main() {
  url := "https://sse-fake.andros.dev/events/"

  resp, err := http.Get(url)
  if err != nil {
    fmt.Println("Error connecting to SSE:", err)
    return
  }
  defer resp.Body.Close()

  if resp.StatusCode != http.StatusOK {
    fmt.Println("Unexpected response status:", resp.Status)
    return
  }

  fmt.Println("Connected to SSE stream...")

  // Create a buffered reader to read the SSE stream
  reader := bufio.NewReader(resp.Body)
  for {
    // Read the next event (usually ending with a newline or empty line)
    line, err := reader.ReadString('\n')
    if err != nil {
      fmt.Println("Error reading SSE stream:", err)
      break
    }

    // Ignore empty lines
    line = strings.TrimSpace(line)
    if line == "" {
      continue
    }

    fmt.Println("Event:", line)

    if line == "exit" {
      fmt.Println("Exiting SSE listener...")
      break
    }
  }
}
```

**Output:**

```
Connected to SSE stream...
Event: :
Event: event: stream-open
Event: data:
Event: event: message
Event: data: {"action": "User connected", "name": "Kelsey"}
Event: event: message
Event: data: {"action": "User connected", "name": "Jennifer"}
Event: event: message
Event: data: {"action": "User disconnected", "name": "Todd"}
Event: event: message
Event: data: {"action": "User connected", "name": "Sandra"}
Event: event: message
Event: data: {"action": "User connected", "name": "Kelly"}
Event: event: message
Event: data: {"action": "User disconnected", "name": "Rachel"}
Event: event: message
Event: data: {"action": "New message", "name": "Vickie", "text": "Skill employee those together painting skin less. Know test drop look report strong late. Easy color they. Current 
never American political."}
```

# Implementing Client Side Web Socket

**1st Method:** Using `github.com/gorilla/websocket`

```go
package main

import (
  "fmt"
  "log"
  "time"

  "github.com/gorilla/websocket"
)

func main() {
  url := "wss://echo.websocket.org/"
  conn, _, err := websocket.DefaultDialer.Dial(url, nil)
  if err != nil {
    log.Fatal(err)
  }
  defer conn.Close()

  count := 0

  go func() {
    for {
      messageType, p, err := conn.ReadMessage()
      if err != nil {
        log.Println(err)
        return
      }

      if messageType == websocket.TextMessage {
        message := string(p)
        log.Printf("Received message: %s\n", message)
      }
    }
  }()

  ticker := time.NewTicker(5 * time.Second)
  defer ticker.Stop()

  for range ticker.C {
    msg := fmt.Sprintf("Count is %d", count)
    err := conn.WriteMessage(websocket.TextMessage, []byte(msg))
    if err != nil {
      log.Println(err)
      return
    }
    log.Println("Sent message: " + msg)
    count++
  }
}
```

**Output:**

```
2025/02/06 11:38:13 Received message: Request served by 1781505b56ee58
2025/02/06 11:38:18 Sent message: Count is 0
2025/02/06 11:38:18 Received message: Count is 0
2025/02/06 11:38:23 Sent message: Count is 1
2025/02/06 11:38:23 Received message: Count is 1
2025/02/06 11:38:28 Sent message: Count is 2
2025/02/06 11:38:28 Received message: Count is 2
2025/02/06 11:38:33 Sent message: Count is 3
2025/02/06 11:38:33 Received message: Count is 3
...
```

**2nd Method:** Using `golang.org/x/net/websocket`

```go
package main

import (
  "fmt"
  "log"
  "time"

  "golang.org/x/net/websocket"
)

func main() {
  url := "wss://echo.websocket.org/"
  conn, err := websocket.Dial(url, "", "http://localhost/")
  if err != nil {
    log.Fatal(err)
  }
  defer conn.Close()

  count := 0

  // Goroutine for receiving messages
  go func() {
    for {
      var msg string
      err := websocket.Message.Receive(conn, &msg)
      if err != nil {
        log.Println(err)
        return
      }
      log.Printf("Received message: %s\n", msg)
    }
  }()

  // Send message every 5 seconds
  ticker := time.NewTicker(5 * time.Second)
  defer ticker.Stop()

  for range ticker.C {
    msg := fmt.Sprintf("Count is %d", count)
    err := websocket.Message.Send(conn, msg)
    if err != nil {
      log.Println(err)
      return
    }
    log.Println("Sent message: " + msg)
    count++
  }
}
```

**Output:**

```
2025/02/06 11:37:02 Received message: Request served by 1781505b56ee58
2025/02/06 11:37:07 Sent message: Count is 0
2025/02/06 11:37:07 Received message: Count is 0
2025/02/06 11:37:12 Sent message: Count is 1
2025/02/06 11:37:12 Received message: Count is 1
2025/02/06 11:37:17 Sent message: Count is 2
2025/02/06 11:37:17 Received message: Count is 2
2025/02/06 11:37:22 Sent message: Count is 3
2025/02/06 11:37:22 Received message: Count is 3
...
```

|  |  |  |
| --- | --- | --- |
| [< Previous Page](../basics/oops.md) | [Home Page](../README.md) | [Next Page >](./files-folders.md) |
|  |  |  |
