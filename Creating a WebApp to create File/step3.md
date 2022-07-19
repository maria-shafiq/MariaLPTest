---
title: 'Defining the structure '

---
<!-- Defining the structure -->

We start by creating a struct that contains the title and body of the txt file. For ease of reference, let us give the struct the name Page.

Add the code below to create the struct and add the imports that will be needed by the program:

```go
package main
 
import (
    "fmt"
    "io/ioutil"
    "log"
    "net/http"
)
 
type Page struct {
    Title string
    Body  []byte
}
{{copy filename='code.go'}}
```

From the code above, `Title` is of type string and, `Body` is of type slice of bytes.

`Body` is represented as slices of bytes instead of string type because it is what the io libraries expect. `Page` struct describes how data will be stored in memory.

Next, we’ll discuss how to store the content of the txt file.