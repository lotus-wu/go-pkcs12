## Introduce

This package code is derived from github.com/AGWA-forks/golang-crypto , and moved to be a independent package for PKCS12 encode and decode!

## Demo

```go
package main

import (
	"io/ioutil"
	"log"
	"strconv"

	"github.com/lotus-wu/go-pkcs12"
)

func main() {
	pfxData, _ := ioutil.ReadFile("a.p12")
	pv, cer, err := pkcs12.DecodeAll(pfxData, "123456")
	if err != nil {
		log.Println(err)
		return
	}
	log.Println(pv)
	log.Println(cer)

	id := int64(0)
	for _, v := range cer {
		filename := "test" + strconv.FormatInt(id, 10) + ".cer"
		ioutil.WriteFile(filename, v.Raw, 0666)
		id += 1
	}

	pfxDataNew, _ := pkcs12.Encode(pv, cer[0], cer[1:], "123456")
	ioutil.WriteFile("1.p12", pfxDataNew, 0666)
}
```

