# Auth Service Client

The auth-service-client is a Go client for interacting with the Auth Service, providing convenient methods to call endpoints like login, token validation, and more.

This client is auto-generated using oapi-codegen based on the OpenAPI specification of the Auth Service.

**Features**

- Login and authentication.
- Token validation and refresh support.
- Predefined request and response types.
- Easily configurable for different environments.

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
	"net/http"

	"github.com/ryanholmesdev/auth-service-client"
)

func main() {
	// Base URL of your Auth Service
	baseURL := "https://auth-service.example.com"

	// Create a new Auth Service Client
	client, err := authserviceclient.NewClientWithResponses(baseURL)
	if err != nil {
		log.Fatalf("Failed to create Auth Service Client: %v", err)
	}

	// Define parameters for GetAuthProviderLogin
	params := &authserviceclient.GetAuthProviderLoginParams{
		RedirectUri: "https://your-app.example.com/callback", // Set your redirect URI
	}

	// Provider for authentication (e.g., "spotify", "tidal")
	provider := "spotify"

	// Make the GetAuthProviderLogin request
	resp, err := client.GetAuthProviderLogin(context.Background(), provider, params)
	if err != nil {
		log.Fatalf("Error calling GetAuthProviderLogin: %v", err)
	}
	defer resp.Body.Close()

	// Process the response
	if resp.StatusCode == http.StatusOK {
		fmt.Println("GetAuthProviderLogin succeeded!")
	} else {
		fmt.Printf("GetAuthProviderLogin failed with status code: %d\n", resp.StatusCode)
	}
}

```
