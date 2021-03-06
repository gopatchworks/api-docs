# Patchworks API

Documentation for patchworks API.

## Table of Contents

- [Introduction](#introduction)
- [Authentication](#quickstart)
- [JWT](#jwt)
- [GraphiQL Sandbox](#graphiql-sandbox)
- [Quickstart Guides](#quickstart-guides)
- [Quickstart for Postman](#quickstart-for-postman)
- [API Response Codes](#api-response-codes)

## Introduction

Our API uses [GraphQL](https://graphql.org/) for data ingestion (mutations) and queries. You can view our online schema using any graphql explorer.

You will need a client ID and a client secret key to access our API. These are used to generate a JSON Web Token (Authorization Bearer) that must be supplied in the HTTP header request. Please keep the client secret private and never include it in source control.

## Authentication

Our API authentication is handled by [Auth0](https://auth0.com/). They have a vast array of SDKs on [Github](https://github.com/auth0). You can sign up for a free account and use it to explore and test OAuth 2.0 and OpenID connect authentication. You will need a valid JSON Web Token to access our API.

## JWT

To generate a JSON Web Token for access.

```bash
CLIENT_ID="YOUR_AUTH0_CLIENT_ID"
CLIENT_SECRET="YOUR_AUTH0_CLIENT_SECRET"
DOMAIN="wearepatchworks.eu.auth0.com"
AUDIENCE="https://sandbox.wearepatchworks.io"
curl --request POST \
  --silent \
  --url "https://$DOMAIN/oauth/token" \
  --header "content-type: application/x-www-form-urlencoded" \
  --data grant_type=client_credentials \
  --data client_id=$CLIENT_ID \
  --data client_secret=$CLIENT_SECRET \
  --data audience=$AUDIENCE
```

You can use https://jwt.io/ to decode and verify your JWT.

You will need to include the HTTP header Authorization Bearer with your JWT to reach endpoints.

```bash
curl --request POST \
  --url https://api.sandbox.wearepatchworks.io/v1/graphql \
  --header "authorization: Bearer ${ACCESS_TOKEN}" \
  --header "content-type: application/json" \
  -d '{"query":"query { pworganization { id name description } }"}'
```

## GraphiQL Sandbox

To view, write, and test mutations and queries in our online GraphiQL sandbox.

```bash
CLIENT_ID="YOUR_AUTH0_CLIENT_ID"
CLIENT_SECRET="YOUR_AUTH0_CLIENT_SECRET"
DOMAIN="wearepatchworks.eu.auth0.com"
AUDIENCE="https://sandbox.wearepatchworks.io"
GRAPHQL_ENDPOINT="https://api.sandbox.wearepatchworks.io/v1/graphql"
ACCESS_TOKEN=$(curl --request POST \
  --silent \
  --url "https://$DOMAIN/oauth/token" \
  --header "content-type: application/x-www-form-urlencoded" \
  --data grant_type=client_credentials \
  --data client_id=$CLIENT_ID \
  --data client_secret=$CLIENT_SECRET \
  --data audience=$AUDIENCE \
  | jq -r .access_token
)
echo "https://cloud.hasura.io/public/graphiql?endpoint=${GRAPHQL_ENDPOINT}&header=Authorization: Bearer ${ACCESS_TOKEN}"
```

Paste the generated link into your browser.

## Quickstart Guides

A collection of useful links to get up and running quickly

- [Auth0's CLI intro](https://www.youtube.com/watch?v=egnVe9lXY0E)
- [Auth0 Next.js quick start](https://github.com/gopatchworks/nextjs-auth0)
- [GraphiQL Sandbox](https://codesandbox.io/s/graphiql-js-example-oc851)

## Quickstart For Postman

- [Auth0 collections for Postman](https://auth0.com/blog/introducing-auth0-collections-for-postman/)
- [GraphQL Quick Start](https://learning.postman.com/docs/sending-requests/supported-api-frameworks/graphql/)
- [Enabling GraphQL auto complete](https://www.postman.com/graphql/)

## API Response Codes

1. 200 - Request successfully recieved. All responses are returned in json, including error codes.
1. 403 - Forbidden. Includes unknown endpoints.
1. 500 - Internal Server Error.
