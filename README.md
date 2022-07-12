# This is ...

demo for gRPC

Thanks to [作ってわかる！ はじめての gRPC](https://zenn.dev/hsaki/books/golang-grpc-starting)

## Preparation

```
brew install protobuf
which protoc
```

```
mkdir demo_grpc
go mod init demo_grpc

go get -u google.golang.org/grpc
go get -u google.golang.org/grpc/cmd/protoc-gen-go-grpc
go install google.golang.org/protobuf/cmd/protoc-gen-go@latest
```

## Generate files

```
cd api
protoc --go_out=../pkg/grpc --go_opt=paths=source_relative \
	--go-grpc_out=../pkg/grpc --go-grpc_opt=paths=source_relative \
	hello.proto
```

## Run server

```
cd cmd/server
go run main.go
```

## Confirmation

Preparation: install grpcurl

```
brew install grpcurl
```

See services

```
$ grpcurl -plaintext localhost:8080 list
grpc.reflection.v1alpha.ServerReflection
myapp.GreetingService
```

See methods in a service

```
$ grpcurl -plaintext localhost:8080 list myapp.GreetingService
myapp.GreetingService.Hello
```

Call a method

```
$ grpcurl -plaintext -d '{"name": "Karaage"}' localhost:8080 myapp.GreetingService.Hello
{
  "message": "Hello, Karaage!"
}
```
