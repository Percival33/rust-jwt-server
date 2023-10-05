# rust-jwt-server

This is a playground repo where I explore rust based on [this](https://youtu.be/6oMoHZZeyb0) tutorial.

It is example JWT authentication using Warp framework.

## Usage

There are two users:

|       | email            | password |
|-------|------------------|----------|
| user  | user@jarcin.dev  | 1234     |
| admin | admin@jarcin.dev | 4321     |

### Login

```bash
curl http://localhost:8000/login -d '{"email": "", "password": ""}' -H 'Content-Type: application/json'
```
This will response with a token which you need to copy in order to use user endpoint

### User Endpoint
First, log in as user

> **To use this endpoint you need to replace `<TOKEN>` with token acquired from login endpoint**

```bash
curl http://localhost:8000/user -H 'Authorization: Bearer <TOKEN>' -H 'Content-Type: application/json'
```
This should be the response: `Hello User 1`

and to this command
```bash
curl http://localhost:8000/admin -H 'Authorization: Bearer <TOKEN>' -H 'Content-Type: application/json'
```
This should be the response after using token from logging as user: ` {"message":"no permission","status":"401 Unauthorized"} `


### Admin Endpoint
First log in as admin.

> **To use this endpoint you need to replace `<TOKEN>` with token acquired from login endpoint**

After using admin endpoint, such as this:
```bash
curl http://localhost:8000/admin -H 'Authorization: Bearer <TOKEN>' -H 'Content-Type: application/json'
```
This should be the response: `Hello Admin 2`

After using user endpoint, such as this:
```bash
curl http://localhost:8000/user -H 'Authorization: Bearer <TOKEN>' -H 'Content-Type: application/json'
```
This should be the response: `Hello User 2`
