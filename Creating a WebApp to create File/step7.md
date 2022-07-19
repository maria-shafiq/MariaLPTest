---
title: 'Create a server and call the handler '

---
<!-- Create a server and call the handler -->

In this step we’ll start our server and define the port it will use to process requests and send responses. We’ll also call the handler and specify the requests’ pathes.

All this will be handled in the `main()` function.

Update the code:

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
 
func viewHandler(w http.ResponseWriter, r *http.Request) {
    title := r.URL.Path[len("/view/"):]
    p, _ := loadPage(title)
    fmt.Fprintf(w, "<h1>%s</h1><div>%s</div>", p.Title, p.Body)
}
*** 
func main() {
    http.HandleFunc("/view/", viewHandler)
    log.Fatal(http.ListenAndServe(":5000", nil))
}
***
{{copy filename='code.go'}}
```

From the code above, the `ListenAndServe()` launches a server that takes and processes requests from port 5000. The `http.HandleFunc()` method has two arguments, `/view/` for the route and `viewHandler()` function of the type `http.HandlerFunc()`.

Before running the app, let's create a mod:

```
go mod init my_mod
{{execute}}
```
Start the server using gin and send the server to the background:

```
nohup  gin --immediate & 
{{execute}}
```

Now, our server is running on port 5000.

View the file "learner.txt" content here:

```
[]('{{webUrl}}' "5000")/view/learner
```

Next, we’ll look at how we can edit the page.