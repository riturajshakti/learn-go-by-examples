# Operating Systems

| [🏠Goto Home](../README.md) | [Goto Bottom🔻](#navigations) |
|---|---|

# Topics

- [run system command](#run-system-command)
- [print info and error logs after running system command](#print-info-and-error-logs-after-running-system-command)
- [exit a program](#exit-a-program)
- [spawn a new process](#spawn-a-new-process)
- [check memory, cpu, platform, and network interface details](#check-memory-cpu-platform-and-network-interface-details)

## run system command

```go
package main

import "os/exec"

func main() {
  // hibernate the system (for windows only)
  cmd := exec.Command("shutdown", "/h")
  cmd.Run()
}
```

**Output:**

```
<Computer will get hibernated>
```

## print info and error logs after running system command

```go
package main

import (
  "fmt"
  "os/exec"
)

func main() {
  cmd := exec.Command("powershell", "ls")

  output, err := cmd.Output()
  if err != nil {
    errorOutput := err.Error()
    fmt.Println("Error executing command:", errorOutput)
  }

  fmt.Println("Output:", string(output))
}
```

**Output:**

```
Output: 

    Directory: C:\Users\ritur\Desktop\My_Works\Learn\Go\go-tutorial


Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
d-----        03-02-2025  11:47 AM                .vscode
d-----        06-02-2025  01:03 PM                advanced
d-----        06-02-2025  07:08 AM                basics
d-----        06-02-2025  02:19 PM                tmp
-a----        05-02-2025  09:14 PM             22 .gitignore
-a----        06-02-2025  11:24 AM            273 go.mod
-a----        06-02-2025  11:24 AM            718 go.sum
-a----        03-02-2025  11:47 AM              0 index.md
-a----        06-02-2025  02:19 PM            294 main.go
-a----        06-02-2025  12:28 PM          10973 README.md
```

## exit a program

**Using os.Exit:**

```go
package main

import (
  "fmt"
  "os"
)

func main() {
  fmt.Println("Going to exit")
  os.Exit(1)
  fmt.Println("This won't run")
}
```

**Output:**

```
Going to exit
```

**Using log.Fatalf:**


```go
package main

import (
  "fmt"
  "log"
)

func main() {
  fmt.Println("Going to exit")
  log.Fatalf("")
  fmt.Println("This won't run")
}
```

**Output:**

```
Going to exit
2025/02/06 14:23:09
```

## spawn a new process

```go
package main

import (
  "fmt"
  "os/exec"
)

func main() {
  // for windows only
  cmd := exec.Command("notepad", "")

  err := cmd.Start()
  if err != nil {
    fmt.Println("Error starting the command:", err)
    return
  }

  err = cmd.Wait()
  if err != nil {
    fmt.Println("Error waiting for command to finish:", err)
    return
  }

  fmt.Println("Command executed successfully")
}
```

**Output:**

```
<opens notepad>
Command executed successfully
```

## check memory, cpu, platform, and network interface details

```go
package main

import (
  "fmt"
  "log"
  "net"
  "runtime"
)

func main() {
  // CPU information
  numCPU := runtime.NumCPU()
  fmt.Printf("CPU Information:\nCores: %d\n", numCPU)

  // Memory information (only total and used from Go runtime)
  var m runtime.MemStats
  runtime.ReadMemStats(&m)
  fmt.Printf("\nMemory Information:\nTotal: %d MB\nUsed: %d MB\n", m.Sys/1024/1024, m.Alloc/1024/1024)

  // Platform Information
  platform := runtime.GOOS
  arch := runtime.GOARCH
  fmt.Printf("\nPlatform Information:\nOS: %s\nArchitecture: %s\n", platform, arch)

  // Network Interface information
  fmt.Println("\nNetwork Interface Information:")
  interfaces, err := net.Interfaces()
  if err != nil {
    log.Fatal("Error getting network interfaces:", err)
  }

  for _, iface := range interfaces {
    // IP addresses for each interface
    addrs, err := iface.Addrs()
    if err != nil {
      log.Println("Error getting IP addresses:", err)
      continue
    }

    fmt.Printf("Interface: %s\n", iface.Name)
    for _, addr := range addrs {
      fmt.Printf("  IP Address: %s\n", addr.String())
    }
  }
}
```

**Output:**

```
CPU Information:
Cores: 12

Memory Information:
Total: 6 MB
Used: 0 MB

Platform Information:
OS: windows
Architecture: amd64

Network Interface Information:
Interface: Local Area Connection* 1
  IP Address: fe80::2c0f:3380:211e:9e42/64
  IP Address: 169.254.40.60/16
Interface: Local Area Connection* 2
  IP Address: fe80::a98f:6887:79b1:6514/64
  IP Address: 169.254.236.122/16
Interface: Wi-Fi
  IP Address: fe80::676:dbfd:12db:ce35/64
  IP Address: 192.168.1.4/24
Interface: Bluetooth Network Connection
  IP Address: fe80::7587:1ac0:3beb:b44b/64
  IP Address: 169.254.74.91/16
Interface: Loopback Pseudo-Interface 1
  IP Address: ::1/128
  IP Address: 127.0.0.1/8
```

# Navigations

| [< Previous Page](./files-folders.md) | [Home Page](../README.md) | [Next Page >](./iterators.md) |
|---|---|---|
