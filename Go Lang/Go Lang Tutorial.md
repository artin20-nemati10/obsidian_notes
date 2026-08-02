## Main Use Case Of GO
- For Performant Application
- Running on scaled distributed systems

## Structure
All our code belong to a package.
The first statement in Go file must be "package …".
A program can only have 1 "main" function, because
you can only have 1 entry point.

"fmt" stands for Format package.

-----------------
### Go Packages
- Go programs are organized into packages.
- Go's standard library provides different core packages for us to use.
- "fmt" is one of these, which you can use by importing it.

###### Example :
```
package main

import "fmt"

func main () {
fmt.Println("Hello World)
}
```

>[!tip] To run the code you should go to terminal and type *"go run main.go"*

#### Variables
- Variables are used to store values.
- Like containers for values.
- Give variable a name & reference everywhere in the app.

#### Benefits
- [x] Update the value only once.
- [x] Make our app more flexible.

##### example :

```
var name = "Artin"

const age = "17"
```

###### Constants
- Constants are like variables, except that their values cannot be changed.

##### Print formatted data
```
fmt.Printf("some text %s with variable \n", my variable)
```

- It takes a template string that contains the text that needs to be formatted

- Plus some annotation verbs or (place holder) that tells the fmt functions how to format the variable passed in.


| Place holder | Work                     |
| ------------ | ------------------------ |
| %s           | For Variables            |
| %v           | For Variables            |
| %T           | For type of the variable |


## 2 Basic Data Types
#### Strings
- For textual data defined with double quotes e.g. "This is a string"
#### Integers
- Representing whole numbers positive and negative.
- There are many more numeric data types.

### Go is a statically typed language
- You need to tell Go Compiler the data types when declaring the variables.
- Type Inference: But Go can infer the type when you assign a value.

## Why so many different data types
1. uint8 : Unsigned 8-bit integers (1 to 255)
2. uint16 : Unsigned 16-bit integers (0 to 65535)
3. uint32 : Unsigned 32-bit integers (1 to 4294967295t)
4. unit64 : Unsigned 64-bit integers (0 to 18446744073709551615)
5. int8 : Signed 8-bit integers (-128 to 127)
6. int16 : Signed 16-bit integers (-32768 to 32767)
7. int32 : Signed 32-bit integers (-2147483648 to 2147483647)
8. int64 : Signed 64-bit integers (-9221172036854775808 to 9221172036854775807)



