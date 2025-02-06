[Goto Home](../README.md)

# sleep for n milliseconds

```go
fmt.Println("Sleeping for 1 sec...")
time.Sleep(1000 * time.Millisecond)
fmt.Println("Done")
```

**Output:**

```
Sleeping for 1 sec...
Done
```

# run a function asynchronously

**Using Channel:**

```go
msg := make(chan string)
go func(message chan string) {
  fmt.Println("From background")
  time.Sleep(time.Second)
  message <- "Hello world"
}(msg)
fmt.Println(<-msg)
```

**Output:**

```
From background
Hello world
```

**Using WaitGroup:**

```go
var wg sync.WaitGroup
msg := ""

wg.Add(1)
go func() {
  defer wg.Done()
  fmt.Println("From background")
  time.Sleep(time.Second)
  msg = "Hello world"
}()
wg.Wait()

fmt.Println(msg)
```

**Output:**

```
From background
Hello world
```

# wait for multiple asynchronous functions to complete

**Using Channels:**

```go
done := make(chan bool, 3)

go func() {
  fmt.Println("1st function started...")
  time.Sleep(3 * time.Second)
  fmt.Println("1st function done")
  done <- true
}()

go func() {
  fmt.Println("2nd function started...")
  time.Sleep(2 * time.Second)
  fmt.Println("2nd function done")
  done <- true
}()

go func() {
  fmt.Println("3rd function started...")
  time.Sleep(1 * time.Second)
  fmt.Println("3rd function done")
  done <- true
}()

<-done
<-done
<-done
fmt.Println("All completed")
```

**Output:**

```
1st function started...
3rd function started...
2nd function started...
3rd function done
2nd function done
1st function done
All completed
```

**Using WaitGroup:**

```go
var wg sync.WaitGroup

wg.Add(1)
go func() {
  defer wg.Done()
  fmt.Println("1st function started...")
  time.Sleep(3 * time.Second)
  fmt.Println("1st function done")
}()

wg.Add(1)
go func() {
  defer wg.Done()
  fmt.Println("2nd function started...")
  time.Sleep(2 * time.Second)
  fmt.Println("2nd function done")
}()

wg.Add(1)
go func() {
  defer wg.Done()
  fmt.Println("3rd function started...")
  time.Sleep(1 * time.Second)
  fmt.Println("3rd function done")
}()

wg.Wait()
fmt.Println("All completed")
```

**Output:**

```
1st function started...
3rd function started...
2nd function started...
3rd function done
2nd function done
1st function done
All completed
```

# wait for at least one asynchronous function to complete

**Using Channels:**

```go
done := make(chan bool, 3)

go func() {
  fmt.Println("1st function started...")
  time.Sleep(3 * time.Second)
  fmt.Println("1st function done")
  done <- true
}()

go func() {
  fmt.Println("2nd function started...")
  time.Sleep(2 * time.Second)
  fmt.Println("2nd function done")
  done <- true
}()

go func() {
  fmt.Println("3rd function started...")
  time.Sleep(1 * time.Second)
  fmt.Println("3rd function done")
  done <- true
}()

<-done
fmt.Println("At least one completed")

<-done
<-done
fmt.Println("Others also completed")
```

**Output:**

```
1st function started...
2nd function started...
3rd function started...
3rd function done
At least one completed
2nd function done
1st function done
Others also completed
```

# passing data between asynchronous function and main function

```go
answer := make(chan int)
go func(result chan int) {
  fmt.Println("calculating result...")
  time.Sleep(1 * time.Second)
  result <- 42
}(answer)
fmt.Println("Result is:", <-answer)
```

**Output:**

```
calculating result...
Result is: 42
```

# perform an operation after some delay

```go
fmt.Println("Timer started...")
ch := time.After(2 * time.Second)
<-ch
fmt.Println("After time completed")
```

**Output:**

```
Timer started...
After time completed
```

# perform an operation after every specific interval

```go
fmt.Println("Timer started...")
ch := time.Tick(1 * time.Second)
count := 3
loop:
  for {
    select {
    case <-ch:
      if count == 0 {
        break loop
      }
      fmt.Println(count)
      count--
    }
  }
fmt.Println("Completed!")
```

**Output:**

```
Timer started...
3
2
1
Completed!
```

# Calculating time interval for any operations

```go
start := time.Now()
for range 100000000 {
}
end := time.Now()
fmt.Println("Time Taken:", end.UnixMilli()-start.UnixMilli(), "ms")
```

**Output:**

```
Time Taken: 84 ms
```

# Thread safe variable

```go
type SafeCounter struct {
  mu  sync.Mutex
  val int
}

func (c *SafeCounter) Increment() {
  c.mu.Lock()
  defer c.mu.Unlock()
  c.val++
}

func (c *SafeCounter) Get() int {
  c.mu.Lock()
  defer c.mu.Unlock()
  return c.val
}

func main() {
  counter := SafeCounter{}
  var wg sync.WaitGroup

  for i := 0; i < 10; i++ {
    wg.Add(1)
    go func() {
      defer wg.Done()
      counter.Increment()
    }()
  }

  wg.Wait()
  fmt.Println("Final count:", counter.Get())
}
```

**Output:**

```
Final count: 10
```

|  |  |  |
| --- | --- | --- |
| [< Previous Page](./errors.md) | [Home Page](../README.md) | [Next Page >](./modules.md) |
|  |  |  |
