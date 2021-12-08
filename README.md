# Project Purple: SteamApi
\*ASP.Net Core(5.0) API

Link to repository: [Link](https://github.com/emiliacs/steamapibackend)

## What is this?

Game library for user, where they can see their steam games.

User can link their Steam Account and see all games they have, and some extra information about those games.

## Requirements

- ASP.Net Core(5.0) [Link](https://dotnet.microsoft.com/download/dotnet/5.0)
- PostgresSQL database (Not tested with other SQL datanbase options yet)

### Install

- Clone and make sure requirements are installed.
- Ethereal email [LINK](https://ethereal.email/)
- Steam Api key. [Link](https://steamcommunity.com/dev/)
- REMEMBER to add appsettings.json!
  - Example

```
{
    "SteamApiKey": "Your steam api key",
    "EmailFrom": "email address",
    "SmtpHost": "hostname",
    "SmtpPort": portnumber,
    "SmtpUser": "user email",
    "SmtpPass": "user password",
    "TokenKey": "token",
    "Logging": {
        "LogLevel": {
            "Default": "Information",
            "Microsoft": "Warning",
            "Microsoft.Hosting.Lifetime": "Information"
        }
    },
    "AllowedHosts": "*"
}
```

- Edit database infromation from statup to match your databse infomation
  - Run update-database in PackageManager when information is correct 
```
update-database
```

## EndPoints

### User

List of endpoints currently available:

| Resource | Endpoint                    | Method | Description                                              |
|----------|-----------------------------|--------|----------------------------------------------------------|
| User     | /register                   | POST   | Register new user                                        |
| User     | /login                      | POST   | User login                                               |
| User     | /users                      | GET    | Get all users                                            |
| User     | /users/{id}                 | PATCH  | Update user email and username by ID                     |
| User     | /users/{id}/changepassword  | PATCH  | Change user password                                     |
| User     | /users/{id}                 | DELETE | Delete user by ID                                        |
| User     | /users/forgottenpassword    | POST   | Send the password reset code to the user's email address |
| User     | /users/resetpassword        | PATCH  | Reset the user's password using the reset code           |
| User     | /users/newverificationcode  | POST   | Send new verification code to user                       |
| User     | /users/verify               | PATCH  | Verify user using the verification code                  |
| User     | /users/{id:long}/addsteamid | PATCH  | Adds Steam ID to the user                                |

### Game

| Resource | Endpoint                    | Method | Description                                              |
|----------|-----------------------------|--------|----------------------------------------------------------|
| Game     | /games/{steamId}                  | PATCH   | Add steam games to user                                    |
| Game     | /games/{appId}                      | PATCH   | Add extra data to steam games                                            |



Input guidelines to POST/PATCH endpoints:

POST /register
```
{
    "email": "youremailhere@example.com",
    "username": "Your username here",
    "password": "YourPasswordHere",
    "confirmpassword": "YourPasswordHere"
}
```

POST /login
```
{
    "email": "youremailhere@example.com",
    "password": "YourPasswordHere"
}
```

PATCH /users/{id}
```
[
    {
        "op": "replace",
        "path": "/email",
        "value": "someemail@example.com"
    },
    {
        "op": "replace",
        "path": "/username",
        "value": "Some Username"
    }
]
```

PATCH /users/{id}/changepassword
```
[
    {
        "op": "replace",
        "path": "/currentpassword",
        "value": "YourPasswordHere"
    },
    {
        "op": "replace",
        "path": "/newpassword",
        "value": "YourNewPasswordHere"
    },
    {
        "op": "replace",
        "path": "/confirmnewpassword",
        "value": "YourNewPasswordHere"
    }
]
```

POST /users/forgottenpassword
```
{
    "email": "someemail@example.com"
}
```

PATCH /users/resetpassword
```
[
    {
        "op": "replace",
        "path": "/email",
        "value": "someemail@example.com"
    },
    {
        "op": "replace",
        "path": "/resetcode",
        "value": "ResetCodeFromYourEmailHere"
    },
    {
        "op": "replace",
        "path": "/newpassword",
        "value": "YourNewPasswordHere"
    },
    {
        "op": "replace",
        "path": "/confirmnewpassword",
        "value": "YourNewPasswordHere"
    }
]
```

POST /users/newverificationcode
```
{
    "email": "someemail@example.com"
}
```

PATCH /users/verify
```
[
    {
        "op": "replace",
        "path": "/email",
        "value": "someemail@example.com"
    },
    {
        "op": "replace",
        "path": "/verificationcode",
        "value": "VerificationCodeFromYourEmailHere"
    }
]
```

PATCH /users/{id}/addsteamid
```
[
{
    "op": "replace",
    "path": "/steamid",
    "value": "XXXXXXXXXXXXXXXXXXXXXXX"
}
]
