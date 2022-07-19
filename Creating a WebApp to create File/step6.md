---
title: Display the file on the server

---
<!--Display the file on the server-->

To display a file content on a web browser, we will add the function `viewHandler()`.

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
 
func loadPage(title string) (*Page, error) {
    filename := title + ".txt"
    body, err := ioutil.ReadFile(filename)
    if err != nil {
        return nil, err
    }
    return &Page{Title: title, Body: body}, nil
}
 
***
func viewHandler(w http.ResponseWriter, r *http.Request) {
    title := r.URL.Path[len("/view/"):]
    p, _ := loadPage(title)
    fmt.Fprintf(w, "<h1>%s</h1><div>%s</div>", p.Title, p.Body)
}
***
{{copy filename='code.go'}}
```

From the code above, the title is extracted from `r.URL.Path`, the path component of the request URL. 
The Path is re-sliced with `[len("/view/"):]` to drop the leading "/view/" component of the request path. This is because the path will invariably begin with "/view/", which is not part of the page's title.

In this case, we will not process the error value returned by the `loadPage()` method. The data loaded, and simple HTML format is introduced to organize how it’s displayed. Lastly it is written to `w`, the `http.ResponseWriter`.

Next, we’ll start the server and call the handler.