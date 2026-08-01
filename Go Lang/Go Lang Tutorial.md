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


