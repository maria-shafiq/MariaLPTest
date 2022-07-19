---
title: Unmarshal structured JSON data

---
<!--Unmarshal structured JSON data-->

```go
package main

import (
	"encoding/json"
	"fmt"
)

type Tent struct {
	Category string
	Color string
}

func main() {
	tentJson := `{"category": "midsized","color": "white"}`
	var tent Tent	
	json.Unmarshal([]byte(tentJson), &tent)
	fmt.Printf("Category: %s, Color: %s", tent.Category, tent.Color)
}
{{copy filename='code.go'}}
```

From the code above, the `[]bytes` from `tentJson` are stored into the address of struct `tent`.

Run the application using the command below to view the output:

```
go run code.go
{{execute}}
```

Next, we’ll look at how we can decode JSON arrays