# Learn Go by Examples

I have created this example sets for you with sample output. This is for those developers who wants to learn go in depth. By following these examples. You can do anything (Literally anything using go).

I have covered a very depth of the language here. Including Basics of Strings/List/Maps, Advanced Concurrency, and many advanced examples including API Call, SSE, Web Sockets, Files/Folders Management, and OS System Calls. Along with many other important topics.

Here is the complete sets of all the topics

# Basics

## Basic Guide

- Learn basic guide from official docs

## [Comments](./basics/comments.md)

- Single Line comments
- Multiline comments

## [Console Input & Output](./basics/console-io.md)

- Print a string on console output
- Print a formatted string on console output
- Print a string on console error
- Print a string without newline character at the end
- Scan a string from console input
- Scan numbers and bool from console input

## [Strings](./basics/strings.md)

- Single line strings
- Multiline strings
- Template Literals/String Interpolation
- Formatted strings
- Accessing the character of string at specific index
- Traversing through a string
- Comparing 2 strings
- Getting string size
- Concatenating strings
- Reversing a string
- Converting a string character into ASCII code
- Converting a ASCII code into string character
- finding substring from index a to b (including a but excluding b)
- finding uppercase of a string
- finding lowercase of a string
- split a string based on specific string
- trimming a string from left side only, right side only, and from both sides
- checking if string has a specific string
- replacing a substring with new string
- finding the index of specific string
- finding the last index of specific string
- check if a string starts with a specific string
- check if a string ends with a specific string
- repeat a string

## [Data Types](./basics/data-types.md)

- Printing the data type of a variable/constant
- Comparing the data type of variable in if-else/switch
- Checking if a variable is an array
- Checking if a variable is a specific object
- Checking if a variable is a function
- dynamic variables

## [Numbers](./basics/numbers.md)

- Create a numeric variable of 1 byte
- finding min between many numbers
- finding max between many numbers
- rounding a number to integer
- rounding a number to `n` digits after decimal points
- finding random number from 0 to 1 (including 0 but excluding 1)
- finding random integer from a to b
- floor of a number
- ceiling of a number
- finding a^b
- finding nth root of a number
- converting a number to string
- converting a string to number
- checking if a numeric string is invalid number (NaN)

## [List/Arrays/Slices](./basics/slices.md)

- List of dynamic data types
- Creating static list
- Creating dynamic list
- Creating list for any type of map
- Getting list size
- Accessing list element at specific index
- Updating list element at specific index
- Removing list element at specific index
- Traversing a list
- Comparing 2 lists based on their contents
- joining array elements in a string
- joining array elements using custom string
- check if an element exist in an array
- find element's index in an array
- find element's index from last in an array
- inserting elements in an array from end
- inserting elements in an array from start
- inserting elements in an array at specific index
- removing n number of elements in an array at specific index
- removing an element from last in an array
- reversing an array
- Clearing the list
- shuffle an array
- Multi-dimensional array (Nested arrays)
- Traversing a multi-dimensional array
- Concatenating 2 arrays into one
- Removing duplicates from an array
- shallow clone an array
- deep clone an array

## [Map](./basics/maps.md)

- Creating an empty map
- Setting key-value pair on a map
- Checking if a key exist in a map
- Accessing value on specific key of map
- Updating value on specific key of map
- Deleting a key-value pair from a map
- Clearing the map
- Getting map size
- Getting keys list of a map
- Getting values list of a map
- Traversing a map
- Merging 2 maps into one

## [Regular Expressions (Regex)](./basics/regex.md)

- Creating a regex from string
- Creating a regex from string with options e.g. `g`, `i`, ...
- Checking if a string follows a regex
- Finding all matching substrings from a string with given regex

## [Operators](./basics/operators.md)

- Increment/Decrement Operators
- Conditional Operators

## [Date and Time](./basics/datetime.md)

- Creating a Date from custom date and time
- Creating a Date from custom timestamps (milliseconds since epoch)
- Creating a Date with current timestamp
- Getting the following details from a Date: year, month, date, hour, minute, second, millisecond, milliseconds since epoch, day of week
- Converting a Date into ISO string
- Create time from iso string
- Adding Day/Hour/Minute/Second/Millisecond to a Date
- Comparing `<`, `>`, `<=`, `>=` and `==` on 2 dates
- Finding the difference between 2 Dates

## [Conditionals & Loops](./basics/conditionals-loops.md)

- Switch where multiple cases executes same statement
- Reverse for loop on numbers
- do-while operations using while loop
- for-each loop on arrays/string
- for-each loop on maps/objects
- for loop on number

## [Functions](./basics/functions.md)

- returning multiple values from a function
- creating function with unlimited parameters
- passing an array elements to a function with unlimited params
- creating anonymous functions
- self invoking function
- creating closures which manages states
- creating higher order functions to replicate:
  - map
  - filter
  - sort
  - forEach
  - some/any
  - every
  - find
  - findIndex
  - reduce
  - group

## [JSON](./basics/json.md)

- converting a data into json string
- converting a data into json string with specific indentation
- converting a typed data into json string
- converting a json string into typed data
- converting a json string into data
- deep clone a data
- validating json string

## [Error/Exception Handling](./basics/errors.md)

- exit a program (throwing errors)
- prevent a program from exit (recover)

## [Concurrency/Delay](./basics/concurrency.md)

- sleep for n milliseconds
- run a function asynchronously
- wait for multiple asynchronous functions to complete
- wait for at least one asynchronous function to complete
- passing data between async function and main function
- perform an operation after some delay
- perform an operation after every specific interval
- Calculating time interval for any operations
- Thread safe variable

## [Packages & Modules](./basics/modules.md)

- creating and using package

## [Object Oriented Programming](./basics/oops.md)

- creating a struct
- creating an anonymous struct
- checking if a property exist in an object
- Traversing through all properties and its details in a struct
- instance methods
- Composition

# Advanced

## [Web Client](./advanced/web-client.md)

- Basic GET api call which returns regular JSON
- POST/PUT/PATCH/DELETE api call with json payload
- Form data upload with files and string fields
- Print file upload percentage
- Set Headers in request payload
- Set URL Search Params in request payload
- Access Response Data:
  - Status code
  - Status message
  - Text Body
  - Json body
  - Headers
- Implementing Client Side SSE (Server Sent Events)
- Implementing Client Side Web Socket

## [Files and Folders](./advanced/files-folders.md)

- Read a text file
- Read a text file line-by-line
- Read a binary file
- Read a binary file in chunks for large files
- Check if file exist
- Create a text/binary file
- Append to a binary file at end
- Append to a binary file at any index
- Copy a file
- Delete a file
- Rename a file
- Move a file
- Create folder
- Delete folder
- Rename folder
- Check if folder exist
- Traverse folder

## [OS](./advanced/os.md)

- run system command
- print info and error logs after running system command
- exit a program
- spawn a new process
- check memory, cpu, platform, and network interface details

## [Iterators](./advanced/iterators.md)

- Creating Iterators

## [Generics](./advanced/generics.md)

- Basic Generic Function

## [Adding 3rd party packages](./advanced/third-party-packages.md)

- Create a project with dependency settings
- Install any 3rd party module to convert markdown into html
- Use that module in your codebase
