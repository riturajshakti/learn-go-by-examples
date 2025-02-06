[Goto Home](../README.md)

# Creating a Date from custom date and time

```go
date := time.Date(2025, time.February, 3, 10, 55, 0, 0, time.UTC)
fmt.Println(date)

date = time.Date(2025, time.February, 3, 10, 55, 0, 0, time.FixedZone("IST", 5.5*60*60))
fmt.Println(date)
```

**Output:**

```
2025-02-03 10:55:00 +0000 UTC
2025-02-03 10:55:00 +0530 IST
```

# Creating a Date from custom timestamps (milliseconds since epoch)

```go
millis := 1738560300000
date := time.UnixMilli(int64(millis))
fmt.Println(date)
```

**Output:**

```
2025-02-03 10:55:00 +0530 IST
```

# Creating a Date with current timestamp

```go
date := time.Now()
fmt.Println(date)
```

**Output:**

```
2025-02-04 11:05:34.2256879 +0530 IST m=+0.000614401
```

# Getting details from date

Getting the following details from a Date: `year`, `month`, `date`, `hour`, `minute`, `second`, `millisecond`, `milliseconds since epoch`, `day of week`

```go
date := time.Now()
fmt.Println("Year:", date.Year())
fmt.Println("Month:", date.Month())
fmt.Println("Day:", date.Day())
fmt.Println("Hour:", date.Hour())
fmt.Println("Minute:", date.Minute())
fmt.Println("Second:", date.Second())
fmt.Println("MilliSecond:", date.Nanosecond()/1000000.0)
fmt.Println("MilliSecond since epoch:", date.UnixMilli())
fmt.Println("Day of week:", date.Weekday())
```

**Output:**

```
Year: 2025
Month: February
Day: 4
Hour: 11
Minute: 12
Second: 48
MilliSecond: 119
MilliSecond since epoch: 1738647768119
Day of week: Tuesday
```

# Converting a Date into ISO string

```go
date := time.Now()
s := date.Format(time.RFC3339)
fmt.Println(s)
```

**Output:**

```
2025-02-04T11:15:01+05:30
```

# Create time from iso string

```go
s := "2025-02-04T11:15:01.876+05:30"
date, _ := time.Parse(time.RFC3339, s)
fmt.Println(date)
```

**Output:**

```
2025-02-04 11:15:01.876 +0530 IST
```

# Adding Day/Hour/Minute/Second/Millisecond to a Date

```go
s := "2025-02-04T22:15:01.876+05:30"
date, _ := time.Parse(time.RFC3339, s)
date = date.Add(24 * time.Hour * 2)   // adding 2 days
date = date.Add(3 * time.Hour)        // adding 3 hours
date = date.Add(10 * time.Minute)     // adding 10 minutes
date = date.Add(2 * time.Second)      // adding 2 seconds
date = date.Add(5 * time.Millisecond) // adding 5 ms
fmt.Println(date)
```

**Output:**

```
2025-02-07 01:25:03.881 +0530 IST
```

# Comparing `<`, `>`, `<=`, `>=` and `==` on 2 dates

```go
a := "2025-02-04T22:15:01+05:30"
b := "2023-02-05T22:15:01+05:30"
date1, _ := time.Parse(time.RFC3339, a)
date2, _ := time.Parse(time.RFC3339, b)
fmt.Println("a == b: ", date1.UnixMilli() == date2.UnixMilli())
fmt.Println("a > b: ", date1.UnixMilli() > date2.UnixMilli())
fmt.Println("a < b: ", date1.UnixMilli() < date2.UnixMilli())
fmt.Println("a <= b: ", date1.UnixMilli() <= date2.UnixMilli())
fmt.Println("a >= b: ", date1.UnixMilli() >= date2.UnixMilli())
fmt.Println("a != b: ", date1.UnixMilli() != date2.UnixMilli())
```

**Output:**

```
a == b:  false
a > b:  true
a < b:  false
a <= b:  false
a >= b:  true
a != b:  true
```

# Finding the difference between 2 Dates

```go
a := "2025-02-04T22:15:01+05:30"
b := "2023-02-05T22:15:01+05:30"
date1, _ := time.Parse(time.RFC3339, a)
date2, _ := time.Parse(time.RFC3339, b)
fmt.Println("a - b: ", date1.UnixMilli()-date2.UnixMilli())
fmt.Println("In days: ", float64(date1.UnixMilli()-date2.UnixMilli())/1000/60/60/24)
```

**Output:**

```
a - b:  63072000000
In days:  730
```
