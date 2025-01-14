---
layout: ballerina-cli-documentation-left-nav-pages-swanlake
title: gRPC
description: The 'Protocol Buffers to Ballerina' tool provides capabilities to generate Ballerina source code for the Protocol Buffer definition.
keywords: ballerina, protocol buffers, programming language
permalink: /learn/cli-documentation/grpc/
active: grpc
intro: The 'Protocol Buffers to Ballerina' tool provides capabilities to generate Ballerina source code for Protocol Buffer definitions.
redirect_from:
  - /learn/how-to-generate-code-for-protocol-buffers
  - /learn/how-to-generate-code-for-protocol-buffers/
  - /learn/generating-ballerina-code-for-protocol-buffer-definitions
  - /swan-lake/learn/generating-ballerina-code-for-protocol-buffer-definitions/
  - /swan-lake/learn/generating-ballerina-code-for-protocol-buffer-definitions
  - /learn/tooling-guide/cli-tools/grpc
  - /learn/tooling-guide/cli-tools/grpc/
  - /learn/cli-documentation/grpc
---

## Usage of the Tool

The code generation tool can produce `ballerina stub` and `ballerina service/client template` files.
 
> In Ballerina, Protocol Buffers serialization is only supported in the gRPC module. Therefore, you can only use
> this tool to generate Ballerina source code for gRPC service definitions.

## CLI Command

You can generate Ballerina source code using the following command:

```
$ bal grpc --input <proto-file-path> [--output <path>] [--mode client | service]
```

### CLI Command Options

`--input`  - Path of the input .proto file. This is a mandatory field. You need to provide the path of the definition
 file.

`--output` - Location of the generated Ballerina source files. This is an optional field. 
If the output path is not specified, the output will be written to a directory corresponding to the package in the Protocol
 Buffers definition. 
If the package is not specified, the output will be written to a 'temp' directory in the current location.

`--mode`   - Set the mode as client or service to generate code samples. If not specified, only the stub file is generated.


## Sample

The below example shows how you can generate Ballerina source code from the following Protocol Buffers definition (in the `helloworld_service.proto` file).

```proto
syntax = "proto3";

service helloWorld {
    rpc sayHello(HelloRequest) returns (HelloResponse);
}

message HelloRequest {
	string name = 1;
}
message HelloResponse {
	string message = 1;
}
```

### Executing the Sample

* Execute the below command to generate the service template file.
```
$ bal grpc --input helloworld_service.proto --mode service --output service
```
Once you execute the command, the stub file (`helloworld_service_pb.bal`) and the service template file (`helloWorld_sample_service.bal`) are generated inside the service directory.
> **Note:** If you have multiple services in a Protocol Buffers definition, this command will generate a stub file with common message types and a service template file for each service definition. This is to avoid duplicating message types in all the service files.


* Execute the below command to generate the client/service stub and client template.
```
$ bal grpc --input helloworld_service.proto --mode client --output client
```
Once you execute the command, the stub file (`helloworld_service_pb.bal`) and the client template file (`helloWorld_sample_client.bal`) are generated inside the client directory.


* Execute the below command to generate only the client/service stub.
```
$ bal grpc --input helloworld_service.proto --output stubs
```
Once you execute the command, only the stub file (`helloworld_service_pb.bal`) is generated inside the `stubs` directory.
