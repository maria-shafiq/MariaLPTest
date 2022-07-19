---
title: Saving changes

---
<!--Saving changes-->

After editing the file, we need a way to save the changes then display them to make sure they are what we expected. We do this by introducing a `saveHandler()` that saves the work and redirects us to the view page.

Add the code below to implement it:

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
 
func editHandler(w http.ResponseWriter, r *http.Request) {
    title := r.URL.Path[len("/edit/"):]
    p, err := loadPage(title)
    if err != nil {
        p = &Page{Title: title}
    }
    renderTemplate(w, "edit", p)
}
 
***
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
    http.HandleFunc("/edit/", editHandler)
***
    http.HandleFunc("/save/", saveHandler)
***    
    log.Fatal(http.ListenAndServe(":5000", nil))
}
{{copy filename='code.go'}}
```

The `saveHandler()` handles the submission of the edit form. It reads the title of the page and the edited body to the new page. The `save()` function is called to save the new changes before redirecting us to the view page.

Our server is running on port 5000.

View the page here:

```
[]('{{webUrl}}' "5000")/edit/learner
```

Next, we’ll look at the key takeaways.