---
title: Marshal struct

---
<!--Marshal struct-->

Marshaling is the process of generating JSON data from a data structure. This process involves converting a converting the data or the objects into a byte-stream.

In the previous steps, we converted structured and unstructured data into JSON using the `unmarshal()` function. In this step, we’ll convert a struct into a JSON object using the `marshal()` function.

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
	smallTent := &Tent {
			Category: "midsized",
			Color: "white",	
		}	

	// encoding the struct to JSON
	data, _ := json.Marshal(smallTent)
	
	// typecasting the output to a string
	fmt.Println(string(data))
}
{{copy filename='code.go'}}
```

From the code above, the struct `smallTent` is converted into a JSON object.

Run the application to view the JSON output:

```
go run code.go
{{execute}}
```

Next, we’ll see how to marshal slices.