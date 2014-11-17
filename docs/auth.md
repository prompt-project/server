# Authentication

Signing up, logging in, checking whether a user is logged in, and logging out.

## Summary

```
HEAD    /auth               # return whether the given credentials are currently logged in
PUT     /auth               # sign up a user with the given credentials
POST    /auth               # log in the user matching the given credentials
DELETE  /auth               # logout the user with the given credentials
PUT     /forgot/:user_id    # send an email with a link to reset your password
PUT     /reset/:token       # sets a user's password. works once per valid token
```

## Signing Up

Creates and logs in a user with the given username, password, and email. Emails and usernames must be unique. Prompt asks for your email so it can send you the email to activate your account. Your username is the handle other users will use to add you as a friend, send you messages, and the handle you'll use to block people or hide them from your timeline.

> Route

```
PUT /auth
```

> Request Body

```javascript
{
    "username": "...",
    "password": "...",
    "email": "..."
}
```

> Response Headers

```
200 OK
Set-Cookie: PromptAuthSession=...
```

Sending the cookie returned in the response headers with future requests will authenticate them as long as the cookie is valid.

If your username or password has already been taken, you'll receive a response like this:

> Response Headers

```
409 Conflict
```

> Response Body

```javascript
{
    "error": {
        "username": "This username has already been taken.",
        "email": "This email has already been taken."
    }
}
```

## Logging In

## Logging Out

## Checking whether a user is logged in