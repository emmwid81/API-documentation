# Fees endpoint
Fee data that can be fetched through the API:

>fee_id<br>
updated<br>
start<br>
minute<br>
discount<br>
penalty<br>

Fetch all price lists:

Requires an admin (or customer?) token.
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
  "fee_id": 1,
  "updated": "2025-10-01T00:00:00.000Z",
  "start": 20,
  "minute": 1,
  "discount": 10,
  "penalty": 15
}
```
Update one or more prices:
>PUT /fees
Required parameters:
>fee_id
JWT token

>Optional parameters:
start
minute
discount
penalty

```javascript
const token = localStorage.getItem('token');
const fees = {
    "start": 21,
    "minute": 2
}
const response = await fetch('/api/v1/fees', {
  method: 'PUT',
  headers: {
    'Authorization': `Bearer ${token}`,
    'Content-Type': 'application/json'
  }
});
const result = await response.json();
```


Optional parameters:
>name<br>
password
```javascript
customer = {
    "password": "drowssap"
}
const response = await fetch("http://localhost:3000/api/v1/customers/4", {
    method: 'PUT',
    body: JSON.stringify(customer),
    headers: {
    'Authorization': `Bearer ${token}`,
    'content-type': 'application/json'
    }
});
const result = await response.json();
```


Result:
```json
{
    "success": true,
    "message": "Customer updated"
}
```