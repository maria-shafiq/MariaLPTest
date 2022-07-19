---
title: Create an edit handler

---
<!--Create an edit handler-->

We’ll now create an editHandler that can use a separate HTML form. To achieve this, we’ll use the `template.ParseFiles()` function just like we did with the `viewHandler()`.

```go
package main
 
import (
    "html/template"
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
 
func renderTemplate(w http.ResponseWriter, tmpl string, p *Page) {
    t, _ := template.ParseFiles(tmpl + ".html")
    t.Execute(w, p)
}
 
func viewHandler(w http.ResponseWriter, r *http.Request) {
    title := r.URL.Path[len("/view/"):]
    p, _ := loadPage(title)
    renderTemplate(w, "view", p)
}

*** 
func editHandler(w http.ResponseWriter, r *http.Request) {
    title := r.URL.Path[len("/edit/"):]
    p, err := loadPage(title)
    if err != nil {
        p = &Page{Title: title}
    }
    renderTemplate(w, "edit", p)
}
***
 
func main() {
    http.HandleFunc("/view/", viewHandler)
***
    http.HandleFunc("/edit/", editHandler)
***
    log.Fatal(http.ListenAndServe(":5000", nil))
}
{{copy filename='code.go'}}
```

From the code above, the `editHnadler()` is called from the `main()` function. The "edit.html" file loaded by the `editHandler` allows us to edit the string contained in the page body. It also gives you an option to save the changes made.

Our server is running on port 5000.

View the page here:

```
[]('{{webUrl}}' "5000")/edit/learner
```

The edit page uses the template from the "edit.html" page.

You can make edits to the template and notice how the HTML page will render differently:

```html
***
<div style="text-align: center;">
***
    <h1>Editing {{.Title}}</h1>
    <form action="/save/{{.Title}}" method="POST">
    <div><textarea name="body" rows="5" cols="40">{{printf "%s" .Body}}</textarea></div><br>
    <div><input type="submit" value="Save"></div>
    </form>
***
</div>
***
{{copy filename='edit.html'}}
```

Then reload the edit page:

```
[]('{{webUrl}}' "5000")/edit/learner
```

Next, we’ll look at how we can edit the page.