
## Installation

1. ```composer require imrancse94/jwt```
2. ```php artisan generate:jwt-secret``` After running the command, it will update `.env` file by below variables.
```bash
JWT_SECRET=<generated-secret>
JWT_ACCESS_TOKEN_EXPIRY=3600 // in seconds
JWT_REFRESH_TOKEN_EXPIRY=84000 // in seconds
```
3. Go to ``config/auth.php`` set driver `jwt`. For example,
```bash
    'guards' => [
        'web' => [
            'driver' => 'session',
            'provider' => 'users',
        ],
        'api' => [
            'driver' => 'jwt',
            'provider' => 'users',
        ]
    ],
```

## Usage
```bash
auth()->attempt($credentials); // it will return access token and refresh token with access token life time.

{
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpYXQiOjE3MjA2MzE3MjMsInR5cGUiOiJhY2Nlc3NfdG9rZW4iLCJleHAiOjE3MjA2MzUzMjMsInBheWxvYWQiOnsiYXV0aF9pZCI6M319.OkiE7tiX1rlAc23rU1zhV6252bODgdma97KfRAjAuo4",
    "expire_in": 3600, // in seconds
    "refresh_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpYXQiOjE3MjA2MzE3MjMsInR5cGUiOiJyZWZyZXNoX3Rva2VuIiwiZXhwIjoxNzIwNzE1NzIzLCJwYXlsb2FkIjp7ImF1dGhfaWQiOjN9fQ.iqiBvcw3ezrBFgR3hVP7aDLPjvge9GLQiTM9MWrA0F8"
}

auth()->refreshToken()  // it will return access token and refresh token with access token life time and user information

{
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpYXQiOjE3MjA2MzMwMjEsInR5cGUiOiJhY2Nlc3NfdG9rZW4iLCJleHAiOjE3MjA2MzY2MjEsInBheWxvYWQiOnsiYXV0aF9pZCI6M319.3kElMASkE2nSJSCvoDq6EzA0zvfISJB5Y2Z-gntfgi4",
    "expire_in": 3600, // in seconds
    "refresh_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpYXQiOjE3MjA2MzMwMjEsInR5cGUiOiJyZWZyZXNoX3Rva2VuIiwiZXhwIjoxNzIwNzE3MDIxLCJwYXlsb2FkIjp7ImF1dGhfaWQiOjN9fQ.c8gfCiLfbUPNSTICtku9SZqFuppOrxg0_zoBLDkyrVQ",
    "user": {
        "id": 3,
        "name": "Imran Hossain",
        "email": "imrancse94@gmail.com",
        "email_verified_at": null,
        "created_at": "2024-06-19T11:54:22.000000Z",
        "updated_at": "2024-06-19T11:54:22.000000Z"
    }
}
```
