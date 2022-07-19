---
title: Load .txt file and start a server

---
<!--Load .txt file and start a server-->

In this step, we will:

- Define the file structure
- Save the file content
- Load file content
- Initiate server and specify the port

Add the following code to implement the above:

```go
package main
 
import (
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
 
func loadPage(title string) (*Page, error) {
    filename := title + ".txt"
    body, err := ioutil.ReadFile(filename)
    if err != nil {
        return nil, err
    }
    return &Page{Title: title, Body: body}, nil
}
 
func main() {
    log.Fatal(http.ListenAndServe(":5000", nil))
}
{{copy filename='code.go'}}
```

From the code above, the Page struct defines the structure of the file. The `save()` method saves the Page's Body to a text file. The `loadPage()` method reads the file's contents into a new variable body and returns a pointer to a Page constructed with the proper title and body values. `ListenAndServe()` launches a server that takes and processes requests from `port 5000`.

Next, we’ll create a template file containing the HTML form.