# TACLink Server

TACLink is an open-source tactical coordination platform that provides real-time situational awareness, secure communication, and cross-organizational coordination capabilities. It serves as a modern alternative to traditional TAK (Tactical Assault Kit) systems, built with Go for improved performance, security, and scalability.

## Core Capabilities

1. **Real-time Situational Awareness**
   - Geospatial mapping and tracking
   - Team position sharing
   - Place/location management
   - Dynamic tactical overlays

2. **Secure Communication**
   - End-to-end encrypted messaging
   - Multi-tenant architecture
   - Role-based access control
   - Device-level authentication

3. **Federation Capabilities**
   - Cross-organization coordination
   - Controlled information sharing
   - Distributed team management
   - Interoperability with existing TAK systems

4. **Modern Architecture**
   - Built in Go for performance and reliability
   - Protocol Buffers for efficient data exchange
   - gRPC for scalable communication
   - Designed for cloud-native deployment

**TAC** stands for **Tactical Adaptive Coordination**, reflecting the system's focus on dynamic adaptability and collaborative functionality within a multi-tenant federated architecture.

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
