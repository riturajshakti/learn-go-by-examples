[Goto Home](../README.md)

# Read a text file

```go
package main

import (
  "fmt"
  "os"
)

func main() {
  content, err := os.ReadFile("example.txt")
  if err != nil {
    fmt.Println("Error reading file:", err)
    return
  }

  fmt.Println(string(content))
}
```

**Output:**

```
Hello Golang
```

# Read a text file line-by-line

```go
package main

import (
  "bufio"
  "fmt"
  "os"
)

func main() {
  filePath := "example.txt"

  file, err := os.Open(filePath)
  if err != nil {
    fmt.Println("Error opening file:", err)
    return
  }
  defer file.Close()

  scanner := bufio.NewScanner(file)
  for scanner.Scan() {
    fmt.Println(scanner.Text())
  }

  if err := scanner.Err(); err != nil {
    fmt.Println("Error reading file:", err)
  }
}
```

**Output:**

```
Hello John
How are you?
```

# Read a binary file

```go
package main

import (
  "fmt"
  "os"
)

func main() {
  file, err := os.Open("temp.pdf")
  if err != nil {
    fmt.Println("Error opening file:", err)
    return
  }
  defer file.Close()

  fileInfo, err := file.Stat()
  if err != nil {
    fmt.Println("Error getting file info:", err)
    return
  }
  fileSize := fileInfo.Size()

  data := make([]byte, fileSize)

  _, err = file.Read(data)
  if err != nil {
    fmt.Println("Error reading file:", err)
    return
  }

  fmt.Printf("Binary data (hex): %x\n", data)
}
```

**Output:**

```
Binary data (hex): 255044462d312e340a25e2e3cfd30a352030206f626a0a3c3c0a2f636120310a2f424d202f4e6f726d616c0a3e3e0a656e646f626a0a392030206f626a0a3c3c0a2f4c656e677468312031363136300a2
```

# Read a binary file in chunks for large files

```go
package main

import (
  "fmt"
  "os"
)

func main() {
  file, err := os.Open("temp.pdf")
  if err != nil {
    fmt.Println("Error opening file:", err)
    return
  }
  defer file.Close()

  chunkSize := 64
  buffer := make([]byte, chunkSize)

  for {
    bytesRead, err := file.Read(buffer)
    if err != nil {
      if err.Error() == "EOF" {
        break
      }
      fmt.Println("Error reading file:", err)
      return
    }

    fmt.Printf("Read %d bytes: %x\n", bytesRead, buffer[:bytesRead])
  }
}
```

**Output:**

```
Read 64 bytes: 255044462d312e340a25e2e3cfd30a352030206f626a0a3c3c0a2f636120310a2f424d202f4e6f726d616c0a3e3e0a656e646f626a0a392030206f626a0a3c3c
Read 64 bytes: 0a2f4c656e677468312031363136300a2f46696c746572202f466c6174654465636f64650a2f4c656e67746820373836330a3e3e0a73747265616d0a789ced7b
Read 64 bytes: 09785445f6efa9baf7f696eef492ad9334e91b3ae9481a0824014288496705268635628204129248409140d81cb7b8201a50184619751c711775d44e824c83ce
Read 51 bytes: 4146373835413643433039443644364630453141393236423e5d0a3e3e0a7374617274787265660a393839370a2525454f460a
```

# Check if file exist

```go
package main

import (
  "fmt"
  "os"
)

func main() {
  _, err := os.Stat("file.txt")
  if err != nil {
    fmt.Println("File does not exists")
  } else {
    fmt.Println("File exists")
  }
}
```

**Output:**

```
File exists
```

# Create a text/binary file

**Creating text file:**

```go
package main

import (
  "fmt"
  "os"
)

func main() {
  file, err := os.Create("example.txt")
  if err != nil {
    fmt.Println("Error creating file:", err)
    return
  }
  defer file.Close()

  _, err = file.WriteString("Hello, World!\n")
  if err != nil {
    fmt.Println("Error writing to file:", err)
    return
  }

  fmt.Println("File created successfully")
}
```

**Output:**

```
File created successfully
```

**Creating binary file:**

```go
package main

import (
  "fmt"
  "os"
)

func main() {
  file, err := os.Create("example.bin")
  if err != nil {
    fmt.Println("Error creating file:", err)
    return
  }
  defer file.Close()

  _, err = file.Write([]byte("Hello, World!\n"))
  if err != nil {
    fmt.Println("Error writing to file:", err)
    return
  }

  fmt.Println("File created successfully")
}
```

**Output:**

```
File created successfully
```

# Append to a binary file at end

```go
package main

import (
  "fmt"
  "os"
)

func main() {
  data := []byte("Bye Bye\n")

  file, err := os.OpenFile("example.bin", os.O_APPEND|os.O_CREATE|os.O_WRONLY, 0644)
  if err != nil {
    fmt.Println("Error opening file:", err)
    return
  }
  defer file.Close()

  _, err = file.Write(data)
  if err != nil {
    fmt.Println("Error writing to file:", err)
    return
  }

  fmt.Println("Binary data appended successfully")
}
```

**Output:**

```
Binary data appended successfully
```

# Append to a binary file at any index

```go
package main

import (
  "fmt"
  "os"
)

func main() {
  filename := "example.bin"
  data := []byte("Nice to see you!")
  index := int64(14) // The position to write at

  file, err := os.OpenFile(filename, os.O_RDWR|os.O_CREATE, 0644)
  if err != nil {
    fmt.Println("Error opening file:", err)
    return
  }
  defer file.Close()

  // Move the file pointer to the desired index
  _, err = file.Seek(index, 0)
  if err != nil {
    fmt.Println("Error seeking in file:", err)
    return
  }

  // Write data at the specified position
  _, err = file.Write(data)
  if err != nil {
    fmt.Println("Error writing to file:", err)
    return
  }

  fmt.Println("Binary data written at index", index, "successfully")
}
```

**Output:**

```
Binary data written at index 14 successfully
```

# Copy a file

```go
package main

import (
  "fmt"
  "io"
  "os"
)

func main() {
  srcFile := "source.txt"
  destFile := "destination.txt"

  // Open the source file
  source, err := os.Open(srcFile)
  if err != nil {
    fmt.Println("Error opening source file:", err)
    return
  }
  defer source.Close()

  // Create the destination file
  destination, err := os.Create(destFile)
  if err != nil {
    fmt.Println("Error creating destination file:", err)
    return
  }
  defer destination.Close()

  // Copy the contents from source to destination
  _, err = io.Copy(destination, source)
  if err != nil {
    fmt.Println("Error copying file:", err)
    return
  }

  fmt.Println("File copied successfully")
}
```

**Output:**

```
File copied successfully
```

# Delete a file

```go
package main

import (
  "fmt"
  "os"
)

func main() {
  err := os.Remove("source.txt")
  if err != nil {
    fmt.Println("Error deleting file:", err)
    return
  }

  fmt.Println("File deleted successfully")
}
```

**Output:**

```
File deleted successfully
```

# Rename a file

```go
package main

import (
  "fmt"
  "os"
)

func main() {
  oldName := "old.txt"
  newName := "new.txt"

  err := os.Rename(oldName, newName)
  if err != nil {
    fmt.Println("Error renaming file:", err)
    return
  }

  fmt.Println("File renamed successfully")
}
```

**Output:**

```
File renamed successfully
```

# Move a file

```go
package main

import (
  "fmt"
  "os"
)

func main() {
  oldPath := "new.txt"
  newPath := "temp/new.txt"

  // Ensure the target directory exists
  err := os.MkdirAll("temp", os.ModePerm)
  if err != nil {
    fmt.Println("Error creating directory:", err)
    return
  }

  // Move (rename) the file
  err = os.Rename(oldPath, newPath)
  if err != nil {
    fmt.Println("Error moving file:", err)
    return
  }

  fmt.Println("Files moved successfully")
}
```

**Output:**

```
Files moved successfully
```

# Create folder

```go
package main

import (
  "fmt"
  "os"
)

func main() {
  path := "temp/category1/test"

  // Create the folder and subdirectory
  err := os.MkdirAll(path, os.ModePerm)
  if err != nil {
    fmt.Println("Error creating directory:", err)
    return
  }

  fmt.Println("Directory created successfully")
}
```

**Output:**

```
Directory created successfully
```

# Delete folder

```go
package main

import (
  "fmt"
  "os"
)

func main() {
  // Remove the folder and its contents
  err := os.RemoveAll("temp")
  if err != nil {
    fmt.Println("Error deleting folder:", err)
    return
  }

  fmt.Println("Folder deleted successfully")
}
```

**Output:**

```
Folder deleted successfully
```

# Rename folder

```go
package main

import (
  "fmt"
  "os"
)

func main() {
  oldPath := "temp"
  newPath := "old"

  err := os.Rename(oldPath, newPath)
  if err != nil {
    fmt.Println("Error renaming folder:", err)
    return
  }

  fmt.Println("Folder renamed successfully")
}
```

**Output:**

```
Folder renamed successfully
```

# Check if folder exist

```go
package main

import (
  "fmt"
  "os"
)

func main() {
  info, err := os.Stat("temp")
  if os.IsNotExist(err) {
    fmt.Println("Folder does not exist")
    return
  }

  if info.IsDir() {
    fmt.Println("Folder exists")
  } else {
    fmt.Println("The path exists, but it is not a folder")
  }
}
```

**Output:**

```
Folder does not exist
```

# Traverse folder

**1st Method:** Traverse at root level of directory only using `os.ReadDir`

```go
package main

import (
  "fmt"
  "os"
)

func main() {
  // Read the directory contents
  entries, err := os.ReadDir("temp")
  if err != nil {
    fmt.Println("Error reading directory:", err)
    return
  }

  // Iterate through the directory entries
  for _, entry := range entries {
    if entry.IsDir() {
      fmt.Println("Directory:", entry.Name())
    } else {
      fmt.Println("File:", entry.Name())
    }
  }
}
```

**Output:**

```
File: list.txt
Directory: test
```

**2nd Method:** Recursively traverse using `filepath.Walk`

```go
package main

import (
  "fmt"
  "os"
  "path/filepath"
)

func main() {
  dir := "temp"

  // Walk through the directory recursively
  err := filepath.Walk(dir, func(path string, info os.FileInfo, err error) error {
    if err != nil {
      fmt.Println("Error accessing", path, err)
      return err
    }

    if info.IsDir() {
      fmt.Println("Directory:", path)
    } else {
      fmt.Println("File:", path)
    }

    return nil
  })

  if err != nil {
    fmt.Println("Error walking the path", err)
  }
}
```

**Output:**

```
Directory: temp
File: temp\list.txt
Directory: temp\test
File: temp\test\ok.txt
```


| [< Previous Page](./web-client.md) | [Home Page](../README.md) | [Next Page >](./os.md) |
|---|---|---|
