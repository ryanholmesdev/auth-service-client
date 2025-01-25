# Auth Service Client

The auth-service-client is a Go client for interacting with the Auth Service, providing convenient methods to call endpoints like login, token validation, and more.

This client is auto-generated using oapi-codegen based on the OpenAPI specification of the Auth Service.

**Features**
* Login and authentication.
* Token validation and refresh support.
* Predefined request and response types.
* Easily configurable for different environments.


## Installation

To install the auth-service-client in your Go project, run:

`go get github.com/ryanholmesdev/auth-service-client@latest`

Or specify a particular version:

`go get github.com/ryanholmesdev/auth-service-client@v1.0.0`

## Usage Example

Here’s a quick example of how to use the auth-service-client:

```go
package main

import (
    "context"
    "fmt"
    "log"
    "github.com/ryanholmesdev/auth-service-client"
)

func main() {
	
    // Base URL of your Auth Service
    baseURL := "https://auth-service.example.com"
    
    // Create a new client
    client, err := authserviceclient.NewClientWithResponses(baseURL)
    if err != nil {
        log.Fatalf("Failed to create client: %v", err)
    }
    
    // Login API example
    resp, err := client.LoginWithResponse(context.Background(), authserviceclient.LoginRequest{
        Username: "exampleuser",
        Password: "examplepassword",
    })
    
    if err != nil {
        log.Fatalf("Failed to call Login API: %v", err)
    }
    
    if resp.JSON200 != nil {
        fmt.Printf("Login successful! Token: %s\n", resp.JSON200.Token)
    } 
    else {
        fmt.Println("Login failed!")
    }
}

```