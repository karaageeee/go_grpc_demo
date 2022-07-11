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
