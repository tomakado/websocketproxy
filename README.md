# WebsocketProxy [![GoDoc](https://pkg.go.dev/github.com/tomakado/websocketproxy?status.svg)](https://pkg.go.dev/github.com/tomakado/websocketproxy) 

WebsocketProxy is an http.Handler interface build on top of
[gorilla/websocket](https://github.com/gorilla/websocket) that you can plug
into your existing Go web server to provide WebSocket reverse proxy.

⚠ **NOTE:** This is a fork of library by [Koding](Koding). Original library seems abandoned. I'm going to support this
fork, so feel free to open your issues and PRs.

## Install

```bash
go get github.com/tomakado/websocketproxy
```

## Example

Below is a simple server that proxies to the given backend URL

```go
package main

import (
	"flag"
	"net/http"
	"net/url"

	"github.com/tomakado/websocketproxy"
)

var (
	flagBackend = flag.String("backend", "", "Backend URL for proxying")
)

func main() {
	u, err := url.Parse(*flagBackend)
	if err != nil {
		log.Fatalln(err)
	}

	if err = http.ListenAndServe(":80", websocketproxy.NewProxy(u)); err != nil {
		log.Fatalln(err)
	}
}
```

Save it as `proxy.go` and run as:

```bash
go run proxy.go -backend ws://example.com:3000
```

Now all incoming WebSocket requests coming to this server will be proxied to
`ws://example.com:3000`

## Differences with original library and TODOs

* Switched to Go modules
* TODO: integrated with GitHub Actions
* TODO: updated tests
* TODO: golangci-lint
* TODO: fixed TODOs in code
