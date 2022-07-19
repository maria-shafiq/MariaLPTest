---
title: Editing pages

---
<!--Editing pages-->

Let’s now edit the pages from our browser.

To do this, we’ll create two new handlers; `editHandler()` and `saveHandler()`.

The edit handler will allow us to edit the page displayed while the save handler will allow us to update the original page with new changes.

Add the code below to implement editing capability:

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
func editHandler(w http.ResponseWriter, r *http.Request) {
    title := r.URL.Path[len("/edit/"):]
    p, err := loadPage(title)
    if err != nil {
        p = &Page{Title: title}
    }
    fmt.Fprintf(w, "<h1>Editing %s</h1>"+
        "<form action=\"/save/%s\" method=\"POST\">"+
        "<textarea name=\"body\">%s</textarea><br>"+
        "<input type=\"submit\" value=\"Save\">"+
        "</form>",
        p.Title, p.Title, p.Body)
}
 
func saveHandler(w http.ResponseWriter, r *http.Request) {
    title := r.URL.Path[len("/save/"):]
    body := r.FormValue("body")
    p := &Page{Title: title, Body: []byte(body)}
    p.save()
    http.Redirect(w, r, "/view/"+title, http.StatusFound)
}
***
 
func main() {
    http.HandleFunc("/view/", viewHandler)
***
    http.HandleFunc("/edit/", editHandler)
    http.HandleFunc("/save/", saveHandler)
***    
    log.Fatal(http.ListenAndServe(":5000", nil))
}
{{copy filename='code.go'}}
```

The function editHandler checks if the page exists, loads it if it’s found, and displays it as HTML form. If it doesn’t exist, the function loads an empty Page struct. The `saveHandler()` fetches the update information and calls on the `save()` method to update the page.

Update the page corresponding to the file "learner.txt" here:

```
[]('{{webUrl}}' "5000")/edit/learner
```

Update the file, save it and you will be redirected to the page "/view/learner" that will show the updated content of the file.

```
[]('{{webUrl}}' "5000")/view/learner
```

You can also check the file content using:

```
cat learner.txt
{{ execute }}
```

If you need to create a new file, let's say a file that has the name "a-new-file.txt", you should visit:

```
[]('{{webUrl}}' "5000")/edit/a-new-file
```

Save it then visualize its content on the server using: 

```
[]('{{webUrl}}' "5000")/view/a-new-file
```

And on the filesystem using:

```
cat a-new-file.txt
{{ execute }}
```

Even if the file doesn't exist, the `saveHandler()` will create it:

```go
func saveHandler(w http.ResponseWriter, r *http.Request) {
    title := r.URL.Path[len("/save/"):]
    body := r.FormValue("body")
    p := &Page{Title: title, Body: []byte(body)}
    p.save()
    http.Redirect(w, r, "/view/" + title, http.StatusFound)
}
```

Next, we’ll look at the key takeaways.