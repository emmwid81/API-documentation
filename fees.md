# Fees endpoint
Fee data that can be fetched through the API:

>fee_id<br>
updated<br>
start<br>
minute<br>
discount<br>
penalty<br>

Fetch all price lists:

>GET /fees/all


```javascript
const token = localStorage.getItem('token');

const response = await fetch('/api/v1/fees/all', {
  method: 'GET',
  headers: {
    'Authorization': `Bearer ${token}`,
    'Content-Type': 'application/json'
  }
});
const result = await response.json();
```

Result:
```json
[
    {
        "fee_id": 1,
        "updated": "2025-10-01T00:00:00.000Z",
        "start": 20,
        "minute": 1,
        "discount": 10,
        "penalty": 15
    },
    {
        "fee_id": 2,
        "updated": "2026-01-14T09:19:35.000Z",
        "start": 200,
        "minute": 1,
        "discount": 10,
        "penalty": 15
    },
    {
        "fee_id": 3,
        "updated": "2026-01-14T09:19:49.000Z",
        "start": 200,
        "minute": 1,
        "discount": 10,
        "penalty": 20
    }
]
```

Fetch current price list:

>GET /fees


```javascript
const token = localStorage.getItem('token');

const response = await fetch('/api/v1/fees', {
  method: 'GET',
  headers: {
    'Authorization': `Bearer ${token}`,
    'Content-Type': 'application/json'
  }
});
const result = await response.json();
```

Result:

```json
{
    "fee_id": 3,
    "updated": "2026-01-14T09:19:49.000Z",
    "start": 200,
    "minute": 1,
    "discount": 10,
    "penalty": 20
}
```

Update one or more prices:

>POST /fees

Requires an admin token.

Required parameters:

>start<br>
minute<br>
discount<br>
penalty


```javascript
const token = localStorage.getItem('token');
const fees = {
    "start": 20,
    "minute": 1,
    "discount": 10,
    "penalty": 15
}
const response = await fetch('/api/v1/fees', {
  method: 'POST',
  body: JSON.stringify(fees),
  headers: {
    'Authorization': `Bearer ${token}`,
    'Content-Type': 'application/json'
  }
});
const result = await response.json();
```

Result:

```json
{
    "success": true,
    "message": "New fees added"
}
```
