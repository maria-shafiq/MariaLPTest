---
title: 'Save the file content '

---
<!-- Save the file content -->

Update the code.go file:

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
 
***
func (p *Page) save() error {
    filename := p.Title + ".txt"
    return ioutil.WriteFile(filename, p.Body, 0600)
}
***
{{copy filename='code.go'}}
```

This method `save()` will save the Page's Body to a text file. 

We will use the txt filename as the Page Title. 

The method takes the file title as the filename for simplicity. It also saves the Page’s Body to a text file. It returns an error type because it is the return type of ioutil.WriteFile(). Another reason for this is to alert the program if anything goes wrong while it's writing the file.

If the method executes everything successfully, it will return nil.

The octal integer literal 0600, which is the parameter in WriteFile, dictates for the file to be created with read-write permissions for the current user only.

Next, now that you’ve saved the file, let’s add the `loadPage` function.