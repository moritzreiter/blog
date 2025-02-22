---
title: "Example for IntelliJ IDEA's HTTP Client"
date: 2024-11-22
---

Here's an example of HTTP requests that can be executed by IntelliJ IDEA's HTTP
client. It gives an overview of the most important features to serve as a quick
reference.

_`dinosaurs.http`_

```

### Get an overview of all dinosaurs (timeout after 60 minutes)
# @timeout 60 m
GET {{apiBaseUrl}}/dionausrs
Accept: application/json

### Get dinosaur by name
GET {{apiBaseUrl}}/dinosaur/brontosaur

### Get all carnivorous dinosaurs
GET {{apiBaseUrl}}/dinosaurs?diet=carnivorous

### Create a new dinosaur
POST {{apiBaseUrl}}/dinosaurs
Content-Type: application/json
Authorization: Bearer {{$auth.token("oauth-staging")}}

{
  "name": "archeopteryx"
}
```

For this to work, two environment config files are needed.

A public one that is meant to get published to the repository alongside the
request file(s):

_`http-client.env.json`_

```json

{
  "staging": {
    "apiBaseUrl": "https://dinosaurs.info/staging-api",
    "tokenUrl": "https://dinosaurs.info/oauth2/token",
    "Security": {
      "Auth": {
        "oauth-staging": {
          "Type": "OAuth2",
          "Grant Type": "Client Credentials",
          "Client ID": "{{clientId}}",
          "Client Secret": "{{clientSecret}}",
          "Token URL": "{{tokenUrl}}",
          "Scope": "dinosaurs"
        }
      }
    }
  },
  "production": {
    "apiBaseUrl": "https://dinosaurs.info/api",
    "tokenUrl": "https://dinosaurs.info/oauth2/token",
    "Security": {
      "Auth": {
        "oauth-staging": {
          "Type": "OAuth2",
          "Grant Type": "Client Credentials",
          "Client ID": "{{clientId}}",
          "Client Secret": "{{clientSecret}}",
          "Token URL": "{{tokenUrl}}",
          "Scope": "dinosaurs"
        }
      }
    }
  }
}
```

And a private one that should not get published to the repository because it
typically contains the necessary secrets for authentication:

_`http-client.private.env.json`_

```json
{
  "staging": {
    "clientId": "abc123",
    "clientSecret": "abcdef123456"
  },
  "production" :{
    "clientId": "abc123",
    "clientSecret": "abcdef123456"
  }
}
```

Storing HTTP requests that are relevant for project in the repository like this
means that every developer will have them available right after cloning it.
Developers who use IntelliJ IDEA can execute them right away to explore the
respective API. But because they are so intiuitively readable, even developers
who don't use IntelliJ IDEA can easily use them as a quick documentation about
the HTTP requests of relevance for the respective project.

I find this much more elegant compared to solutions like Postman or Insomnia.

