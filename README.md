# TAC Server

A gRPC server for handling tactical observations and authentication.

## Prerequisites

- Go 1.23.1 or later
- Protocol Buffers v5.29.3 or later
- `protoc-gen-go` v1.36.4 or later
- `protoc-gen-go-grpc` v1.5.1 or later

## Installation

1. Install Protocol Buffers:
   ```bash
   # For macOS
   brew install protobuf

   # For Linux
   apt-get install protobuf-compiler
   ```

2. Install Go protocol buffer plugins:
   ```bash
   go install google.golang.org/protobuf/cmd/protoc-gen-go@v1.36.4
   go install google.golang.org/grpc/cmd/protoc-gen-go-grpc@v1.5.1
   ```

3. Clone the repository:
   ```bash
   git clone https://github.com/sonoran-softworks/tac-server.git
   cd tac-server
   ```

4. Install dependencies:
   ```bash
   go mod tidy
   ```

## Generate Protocol Buffer Code

The project uses protocol buffers for service definitions. To regenerate the protobuf code:
```bash
# Generate observation service
protoc --go_out=. --go_opt=paths=source_relative \
    --go-grpc_out=. --go-grpc_opt=paths=source_relative \
    proto/observation/observation.proto

# Generate auth service
protoc --go_out=. --go_opt=paths=source_relative \
    --go-grpc_out=. --go-grpc_opt=paths=source_relative \
    proto/auth/auth.proto
```

## Project Structure

```
.
├── main.go                 # Server entry point
├── proto/                  # Protocol buffer definitions
│   ├── auth/              # Authentication service
│   └── observation/       # Observation service
├── server/                # Server implementations
│   ├── auth_server.go     # Auth service implementation
│   ├── middleware.go      # gRPC middleware
│   └── observation_server.go  # Observation service implementation
└── types/                 # Common type definitions
```

## Running the Server

To start the server:

```bash
go run main.go
```

The server will listen on port 50051 by default.

## Authentication

The server uses Ed25519 public key authentication. Clients must:
1. Generate an Ed25519 key pair
2. Sign a timestamp with their private key
3. Send the public key, signature, and timestamp in the login request
4. Use the returned token in the "authorization" metadata for subsequent requests

## Services

### Auth Service
- `Login`: Authenticates users and provides access tokens

### Observation Service
- `CreateObservation`: Creates a new observation with associated events

## Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## License

[Add your license information here]
