---
title: Marshal slices

---
<!--Marshal slices-->

This is achieved by encoding the slice passed using the `json.Marshal` function.

The program below takes slices and prints out JSON data:

```go
package main

import (
	"encoding/json"
	"fmt"
)

type Tent struct {
	Category string `json:"size"`
	Color string `json:"color"`
}

func main() {
	tentOne := &Tent {
			Category: "midsized",
			Color: "white",	
		}
	tentTwo := &Tent {
			Category: "small",
			Color: "blue",	
		}	

	// encoding the slice to JSON
	data, _ := json.Marshal([]*Tent{tentOne, tentTwo})
	
	// typecasting the output to a string
	fmt.Println(string(data))
}
{{copy filename='code.go'}}
```

The program creates a slice of structs. The slice is then marshaled and typecasted to a string.

Run the code to view the JSON output:

```
go run code.go

{{execute}}
```

Next, we’ll look at how to marshal maps.