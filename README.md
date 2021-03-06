goreferrer
==========

A Go package that analyzes and classifies different kinds of referrer URLs (search, social, ...).

## Example

```
package main

import (
	"fmt"
	"github.com/Shopify/goreferrer"
)

var urls = []string{
	"http://ca.search.yahoo.com/search?p=hello",
	"https://twitter.com/jdoe/status/391149968360103936",
	"http://yoursite.com/links",
}

func main() {
	for _, url := range urls {
		r, err := referrer.Parse(url)
		if err != nil {
			panic(err)
		}
		switch r := r.(type) {
		case *referrer.Search:
			fmt.Printf("Search %s: %s\n", r.Label, r.Query)
		case *referrer.Social:
			fmt.Printf("Social %s\n", r.Label)
		case *referrer.Indirect:
			fmt.Printf("Indirect: %s\n", r.Url)
		}
	}
}
```
Result:
```
Search Yahoo: hello
Social Twitter
Indirect: http://yoursite.com/links
```
