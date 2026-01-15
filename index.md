# REST API for spark - a system for escooter rentals

This API was constructed as a part of a team project for the course "vteam" given at Blekinge Tekniska Högskola.

The project - a system for e-scooter rentals - can be viewed on GitHub: [spark](https://github.com/lohengrin1337/spark
)

The API endpoints require authentication in the form of a valid JWT (Json Web Token) with different levels authorization built into it.

Admin tokens give full access to the API while customer tokens allows access to a more limited number of endpoints and also requires the user id encoded into the token to match the user id of the requested data. (A customer may never access user information belonging to another customer.) Third party applications and vehicles are also authenticated with tokens and may access a few select endpoints. A rate limiter is applied to all individual requests/tokens to avoid any abuse or attacks which may slow down or harm the system.

Input from users is validated before the request can be processed further to avoid corrupting the database.

The tokens are signed using a secret and contain information about the authenticated user:
```json
{
    "id": <id>,
    "role": <customer, admin etc>,
    "iat": <issued at, timestamp>,
    "exp": <expiration time>
}
```

## Endpoints:
1. [auth](https://emmwid81.github.io/API-documentation/auth)
2. [bikes](https://emmwid81.github.io/API-documentation/bikes)
3. [cities](https://emmwid81.github.io/API-documentation/cities)
4. [customers](https://emmwid81.github.io/API-documentation/customers)
5. [fees](https://emmwid81.github.io/API-documentation/fees)
6. [invoices](https://emmwid81.github.io/API-documentation/invoices)
7. [rentals](https://emmwid81.github.io/API-documentation/rentals)
8. [zones](https://emmwid81.github.io/API-documentation/zones)

