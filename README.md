# gconcat

[![GoDoc][1]][2]
[![GitHub release][3]][4]
[![Coverage Status][5]][6]
[![Build Status][7]][8]
[![Go Report Card][9]][10]
[![License][11]][11]

[1]: https://godoc.org/github.com/jeffotoni/gconcat?status.svg
[2]: https://godoc.org/github.com/jeffotoni/gconcat
[3]: https://img.shields.io/github/v/release/jeffotoni/gconcat?include_prereleases
[4]: https://github.com/jeffotoni/gconcat/releases
[5]: https://coveralls.io/repos/github/jeffotoni/gconcat/badge.svg?branch=master
[6]: https://coveralls.io/github/jeffotoni/gconcat?branch=master
[7]: https://travis-ci.com/jeffotoni/gconcat.svg?branch=master
[8]: https://travis-ci.com/jeffotoni/gconcat
[9]: https://goreportcard.com/badge/github.com/jeffotoni/gconcat
[10]: https://goreportcard.com/report/github.com/jeffotoni/gconcat
[11]: https://img.shields.io/github/license/jeffotoni/gconcat

>A simple lib for concatenation, it accepts several types as a parameter and returns a string. A battery of tests was done, there are some complexities that we cannot escape to have the best computational cost 

## Example 

#### Concatenating some basic types in Go
```go
package main

import (
	g "github.com/jeffotoni/gconcat"
)

func main() {
	// accepting all types 
	str := g.Concat("/api/v1", "/", 39383838, "/", 129494, "/product/", 2012)
	println(str)

	// accepting only string
	str := g.ConcatStr("jeffotoni", "/", "2021", "/", "product")
	println(str)

	// accepting only string and int
	str := g.ConcatStrInt("jeffotoni", "/", 2021, "/", "product", "/", 1001)
	println(str)
}
```

#### Concatenating types using interfaces
```go
package main

import (
	g "github.com/jeffotoni/gconcat"
)

func main() {
	var ii []interface{}
	ii = append(ii, "jeffotoni")
	ii = append(ii, " ")
	ii = append(ii, "joao")
	ii = append(ii, " ")
	ii = append(ii, 2021)

	var i interface{}
	i  = "jeffotoni"

	println(g.Concat(ii))
	println(g.Concat(i))
	println(g.Concat("jeffotoni", "&", "joao", " ", 20, "/08/"))
	println(g.Concat([]string{"2017", " ", "2018", " ", "2020"}))
	println(g.Concat([]int{12, 0, 11, 0, 10, 11, 12, 23, 3}))
	println(g.Concat(10,9,10,20,30,40,"x", "&", "."))
	println(g.Concat("R$ ",23456.33, " R$ ",123.33, " R$ ",19.11))
}
```

## Example on your project 
```go
package main

import (
	"log"
	"net/http"

	g "github.com/jeffotoni/gconcat"
)

const PORT = ":8282"

func main() {
	mux := http.NewServeMux()
	mux.HandleFunc("/ping",
		func(w http.ResponseWriter, r *http.Request) {
			str := g.Concat(
                            []int{1, 2, 3, 4, 5}, " ", 
                            []string{"Let's test our concat!!!"},
                    )
		w.Write([]byte(str))
		})
	    
	server := &http.Server{
		Addr:    PORT,
		Handler: mux,
	}
	println("Start Run: ", PORT)
	log.Fatal(server.ListenAndServe())
}

```

### Some types allowed
> - bool
> - int
> - int32
> - int64
> - interface
> - string
> - uint
> - float32
> - float64
> - []int
> - []int32
> - []int64
> - []interface
> - []string
> - []uint
> - []float32
> - []float64

## Install Using go mod in your project
```bash
$ go mod init <your-dir>
$ go mod tidy
$ go run main.go
``````

#### Another possibility would be
```bash
$ go get -u github.com/jeffotoni/gconcat
```

#### Test Benchmarking

```bash
$ go test -bench . -benchmem
goarch: amd64
pkg: github.com/jeffotoni/gconcat
cpu: Intel(R) Core(TM) i7-10750H CPU @ 2.60GHz
BenchmarkStringPlus-12         	12953655	        91.08 ns/op	     416 B/op	       1 allocs/op
BenchmarkConcatStr-12          	11909199	       106.1 ns/op	     416 B/op	       1 allocs/op
BenchmarkConcatStrInt-12       	 3907837	       310.4 ns/op	     952 B/op	       7 allocs/op
BenchmarkConcat-12             	 3916066	       320.3 ns/op	     976 B/op	       8 allocs/op
BenchmarkConcatIntString-12    	 5969743	       212.5 ns/op	     128 B/op	       6 allocs/op
BenchmarkLongJoin-12           	11099569	       108.5 ns/op	     448 B/op	       1 allocs/op
BenchmarkLongSprintf-12        	 4332783	       327.4 ns/op	     480 B/op	       5 allocs/op
BenchmarkBuilder-12            	 5473576	       207.1 ns/op	    2201 B/op	       0 allocs/op
BenchmarkConcatVector-12       	  237378	      5200 ns/op	    4616 B/op	      84 allocs/op
BenchmarkMarshal-12            	  382440	      2939 ns/op	     768 B/op	       1 allocs/op
PASS
ok  	github.com/jeffotoni/gconcat	14.925s
```

#### Creators

Jefferson Otoni, [@jeffotoni](https://twitter.com/jeffotoni), [github.com/jeffotoni](https://github.com/jeffotoni), [linkedin.com/in/jeffotoni](https://www.linkedin.com/in/jeffotoni)   

João Vitor – [@ancogamer](https://twitter.com/ancogamer), [github.com/ancogamer](https://github.com/ancogamer), [linkedin.com/in/joão-vitor-astori-saletti](https://www.linkedin.com/in/joão-vitor-astori-saletti)


Distributed under the MIT license. See ``LICENSE`` for more information.

## Contributing

To contribuit is simples, just clone or fork the repository and send to us the pull request
