
```sh
$ go build -o agent cmd/agent/main.go
$ go build -o proxy cmd/proxy/main.go

# Build for Windows
$ GOOS=windows go build -o agent.exe cmd/agent/main.go
$ GOOS=windows go build -o proxy.exe cmd/proxy/main.go
```