
# gRPC Protos

This repository contains the Protocol Buffers (`.proto`) definitions and generated gRPC code.

## Table of Contents
- [Overview](#overview)
- [Directory Structure](#directory-structure)
- [Requirements](#requirements)
- [How to Generate Code](#how-to-generate-code)

## Overview
This repository serves as the source of truth for the `.proto` files used in our gRPC-based microservices. It includes:
- `.proto` definitions.
- Scripts and tools for generating gRPC and Go code.

## Directory Structure
```plaintext
.
├── proto/                     # Directory containing .proto files
│   └── sso/                   # Example service
│       └── sso.proto           
├── gen/                       # Generated Go code
│   └── go/
│       └── sso/               # Generated code for sso.proto
│           ├── sso_grpc.pb.go
│           └── sso.pb.go
├── go.mod                     # Go module definition file
├── go.sum                     # Dependency checksum file
└── Taskfile.yaml              # Automation tasks
```

## Requirements
To work with this repository, ensure you have the following installed:

1. **Protocol Buffers Compiler (`protoc`)**:
   - Version 3.20 or higher.
   - [Installation guide](https://grpc.io/docs/protoc-installation/).

2. **Go Plugins for Protobuf**:
   Install these tools for generating Go code:
   ```bash
   go install google.golang.org/protobuf/cmd/protoc-gen-go@latest
   go install google.golang.org/grpc/cmd/protoc-gen-go-grpc@latest
   ```

3. **Task Runner (Optional)**:
   Install [Task](https://taskfile.dev/) to simplify running commands:
   ```bash
   sudo sh -c "$(curl --location https://taskfile.dev/install.sh)" -- -d /usr/local/bin
   ```

## How to Generate Code

### Using `protoc` Manually
Run the following command to generate Go code from `.proto` files:
```bash
protoc -I proto proto/sso/*.proto \
  --go_out=./gen/go/ \
  --go_opt=paths=source_relative \
  --go-grpc_out=./gen/go/ \
  --go-grpc_opt=paths=source_relative
```

### Using Taskfile
If you have `Task` installed, simply run:
```bash
task generate
```

This will:
- Compile `.proto` files in the `proto/sso/` directory.
- Place the generated Go files in the `gen/go/` directory.

### Cleaning Generated Code
To remove previously generated files:
```bash
task clean
```
