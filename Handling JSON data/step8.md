---
title: Marshal a map

---
<!--Marshal a map-->

Marshaling data to maps is reserved for the use case when the data is unstructured.

The values on the map can be any serialized type while the key needs to be a string or a type that can be converted to a string.

Below is an example that marshals a map:

```go
package main

import (
	"encoding/json"
	"fmt"
)

func main() {
	vehicle := map[string]interface{}{
		"Cars": map[string]string{
			"Honda CRV":     "30000",
			"Mercedes C200": "41000",
		},
		"motocycles": "none",
	}
	data, _ := json.Marshal(vehicle)
	fmt.Println(string(data))
}

{{copy filename='code.go'}}
```

From the code above, the map is converted using the marshal() function.

Run the program to view the JSON output:

```
go run code.go
{{execute}}
```

Next, we’ll look at the key takeaways.