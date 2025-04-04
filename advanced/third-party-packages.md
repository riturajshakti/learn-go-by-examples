# Third Party Packages

| [🏠Goto Home](../README.md) | [Goto Bottom🔻](#navigations) |
|---|---|

# Topics

- [Sample program to convert markdown into html](#sample-program-to-convert-markdown-into-html)
- [Install a package to convert markdown to html](#install-a-package-to-convert-markdown-to-html)
- [Use the package module in the codebase](#use-the-package-module-in-the-codebase)

## Sample program to convert markdown into html

- Create a folder named `md2html`

- Open this folder in command line

- Initialize the go project

```sh
go mod init md2html
```

## Install a package to convert markdown to html

```sh
go get github.com/gomarkdown/markdown
```

## Use the package module in the codebase

```go
package main

import (
  "fmt"

  "github.com/gomarkdown/markdown"
)

var md string = `
# Welcome to Golang

Hi, Welcome to Go programming language

## Go Tour

Here you will learn go

## Topics

- Strings
- List
- Map
- Concurrency

## Sample Go Code

` + "```" + `go
package main

import (
  "fmt"
)

func main() {
  fmt.Println("Hello World!")
}
` + "```"

func main() {
  html := markdown.ToHTML([]byte(md), nil, nil)
  fmt.Println(string(html))
}
```

**Output:**

```
<h1>Welcome to Golang</h1>

<p>Hi, Welcome to Go programming language</p>

<h2>Go Tour</h2>

<p>Here you will learn go</p>

<h2>Topics</h2>

<ul>
<li>Strings</li>
<li>List</li>
<li>Map</li>
<li>Concurrency</li>
</ul>

<h2>Sample Go Code</h2>

<pre><code class="language-go">package main

import (
        &quot;fmt&quot;
)

func main() {
        fmt.Println(&quot;Hello World!&quot;)
}
</code></pre>
```

# Navigations

| [< Previous Page](./generics.md) | [Home Page](../README.md) | Next Page > |
|---|---|---|
