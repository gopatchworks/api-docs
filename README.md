# Patchworks API

Documentation for patchworks API.

## Table of Contents

- [Introduction](#introduction)
- [Authentication](#quickstart)
- [JWT](#jwt)
- [GraphiQL Sandbox](#graphiql-sandbox)
- [Quickstart Guides](#quickstart-guides)

## Introduction

## Authentication

Our API authentication is handled by https://auth0.com/. They have a vast array of SDKs on github https://github.com/auth0 You can sign up for a free account with them and use it to explore and debug OAuth 2.0 and OpenID connect. You will need a valid JSON Web Token to access our API.

## JWT

To generate a JSON Web Token for access.

```bash
# 
YOUR_DOMAIN=wearepatchworks.eu.auth0.com
YOUR_CLIENT_ID='YOUR_AUTH0_CLIENT_ID'
YOUR_CLIENT_SECRET='YOUR_AUTH0_CLIENT_SECRET'
YOUR_API_IDENTIFIER="https://api.eudo1.wearepatchworks.io"
curl --request POST \
  --silent \
  --url "https://$YOUR_DOMAIN/oauth/token" \
  --header "content-type: application/x-www-form-urlencoded" \
  --data grant_type=client_credentials \
  --data client_id=$YOUR_CLIENT_ID \
  --data client_secret=$YOUR_CLIENT_SECRET \
  --data audience=$YOUR_API_IDENTIFIER
```

You can use https://jwt.io/ to decode and verify your JWT.

## GraphiQL Sandbox

To view, write, and test mutations and queries in our online GraphiQL sandbox.

```bash
DOMAIN=wearepatchworks.eu.auth0.com
CLIENT_ID='YOUR_AUTH0_CLIENT_ID'
CLIENT_SECRET='YOUR_AUTH0_CLIENT_SECRET'
API_ENDPOINT="https://api.eudo1.wearepatchworks.io"
GRAPHQL_ENDPOINT="${API_ENDPOINT}/v1/graphql"
ACCESS_TOKEN=$(curl --request POST \
  --silent \
  --url "https://$DOMAIN/oauth/token" \
  --header "content-type: application/x-www-form-urlencoded" \
  --data grant_type=client_credentials \
  --data client_id=$CLIENT_ID \
  --data client_secret=$CLIENT_SECRET \
  --data audience=$API_ENDPOINT \
  | jq -r .access_token
)
echo "https://cloud.hasura.io/public/graphiql?endpoint=https://talented-flamingo-73.hasura.app/v1/graphql&header=Authorization: Bearer ${ACCESS_TOKEN}"
```

Paste the generated link into your browser.

## Quickstart Guides

A collection of useful links to get up and running quickly

- [Auth0's CLI intro](https://www.youtube.com/watch?v=egnVe9lXY0E)
- [Auth0 Next.js quick start](https://github.com/gopatchworks/nextjs-auth0)
- [GraphiQL Sandbox](https://codesandbox.io/s/graphiql-js-example-oc851)
