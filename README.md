# What is the Regexp Map

The Regexp Map is a specify Map. Its key can is a string or a a regexp. when the index is string. It will to index the string. If it didn't match. It will to match the regexp.

# Note
- Require Regexp is independent.
- No Thread Safe

# Usage 
```go  
package main

import (
	"fmt"

	"github.com/CorrectRoadH/regexp_map"
)

func main() {
	testMap := regexp_map.NewRegexHashMap[string]()
	testMap.SetStringKey("https://youtube.com", "youtube")
	testMap.SetStringKey("https://bilibili.com", "bilibili")
	testMap.SetRegexpKey("^https?://(?:www\\.)?bilibili\\.com(/[\\w-]+)*/?(\\?[^#]*)?(#.*)?$", "bilibili")

	result1, ok, key := testMap.Get("https://youtube.com")
	fmt.Println(result1, ok, key) // youtube true https://youtube.com

	result2, ok, _ := testMap.Get("https://bilibili.com")
	fmt.Println(result2, ok) // bilibili true

	result3, ok, key := testMap.Get("https://www.bilibili.com/video/BV1394y1k7D2/")
	fmt.Println(result3, ok, key) // bilibili true ^https?://(?:www\.)?bilibili\.com(/[\w-]+)*/?(\?[^#]*)?(#.*)?$

	result4, ok, key := testMap.Get("https://discord.com")
	fmt.Println(result4, ok, key) //  false
}
```