# Auth Service Client

The auth-service-client is a Go client for interacting with the Auth Service.

This client is auto-generated using oapi-codegen based on the OpenAPI specification of the Auth Service.

**Features**

-- All endpoints from the Auth Service are available here

## Installation

To install the auth-service-client in your Go project, run:

`go get github.com/ryanholmesdev/auth-service-client@latest`

Or specify a particular version:

`go get github.com/ryanholmesdev/auth-service-client@v1.0.0`

## Usage Example

Here’s a quick example of how to use the auth-service-client:

Other methods can be found in the client itself

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

	// Set the Url for the client to point too
	baseURL := "https://auth-service.example.com"

	// Create a new Auth Service Client
	client, err := authserviceclient.NewClientWithResponses(baseURL)
	if err != nil {
		log.Fatalf("Failed to create Auth Service Client: %v", err)
	}

	// Define parameters for GetAuthProviderLogin
	params := &authserviceclient.GetAuthProviderLoginParams{
		RedirectUri: "https://your-app.example.com/callback", 
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
