---
title: Loading the page

---
<!--Loading the page-->

Update the application by adding `loadPage`:

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
 
func (p *Page) save() error {
    filename := p.Title + ".txt"
    return ioutil.WriteFile(filename, p.Body, 0600)
}
 
***
func loadPage(title string) (*Page, error) {
    filename := title + ".txt"
    body, err := ioutil.ReadFile(filename)
    if err != nil {
        return nil, err
    }
    return &Page{Title: title, Body: body}, nil
}
***
{{copy filename='code.go'}}
```

`loadPage()` has title (of type string) as the receiver value. It uses the title to construct the filename. It uses `ReadFile()` read it. The `ReadFile()` function has two return values, `[]bytes` and `error`.

We now have a defined data structure, and the ability to save as well as load the file.

Next, we’ll use net/http package to serve the loaded file.