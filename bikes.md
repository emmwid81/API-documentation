
## 2. Bikes endpoint

All routes require a jwt token.<br>
Some routes require a jwt token with role: admin.

The GET /bikes route can return bikes filtered on one or more of the query parameters city=\<city>, status=\<bike status>, zone_type=\<zone type>. Unless called with parameter status=deleted it always omits deleted bikes.

Bike data that can be fetched from the database:

>bike_id<br>
city<br>
status<br>
coordinates<br>

Fetch all bikes:
>GET /bikes

Requires admin token.

```javascript
const token = localStorage.getItem('token');

const response = await fetch('/api/v1/bikes', {
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
        "bike_id": 1,
        "city": "Malmö",
        "status": "needCharging",
        "coordinates": {
            "type": "Point",
            "coordinates": [
                13.0040145,
                55.6090932
            ]
        },
        "zones": [
            {
                "zone_id": 1,
                "zone_type": "city"
            },
            {
                "zone_id": 2,
                "zone_type": "slow"
            }
        ]
    },
    {
        "bike_id": 2,
        "city": "Malmö",
        "status": "active",
        "coordinates": {
            "type": "Point",
            "coordinates": [
                12.99335,
                55.6058207
            ]
        },
        "zones": [
            {
                "zone_id": 1,
                "zone_type": "city"
            },
            {
                "zone_id": 2,
                "zone_type": "slow"
            }
        ]
    },
  ... ]
```

Fetch one bike by id:

> GET /bikes/:id

```javascript
const token = localStorage.getItem('token');

const response = await fetch('/api/v1/bikes/5', {
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
    "bike_id": 5,
    "city": "Malmö",
    "status": "deleted",
    "coordinates": {
        "type": "Point",
        "coordinates": [
            13.0261374,
            55.6070085
        ]
    },
    "zone_id": 1,
    "zone_type": "city"
}
```
Fetch all bikes belonging to a city:

Requires admin token.

>GET /bikes?city=\<city>

```javascript
const token = localStorage.getItem('token');

const response = await fetch('/api/v1/bikes?city=malmö', {
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
        "bike_id": 3,
        "city": "Malmö",
        "status": "needCharging",
        "coordinates": {
            "type": "Point",
            "coordinates": [
                12.9972124,
                55.5979654
            ]
        },
        "zones": [
            {
                "zone_id": 1,
                "zone_type": "city"
            },
            {
                "zone_id": 2,
                "zone_type": "slow"
            }
        ]
    },
    {
        "bike_id": 4,
        "city": "Malmö",
        "status": "needCharging",
        "coordinates": {
            "type": "Point",
            "coordinates": [
                13.0310297,
                55.5998566
            ]
        },
        "zones": [
            {
                "zone_id": 1,
                "zone_type": "city"
            },
            {
                "zone_id": 2,
                "zone_type": "slow"
            }
        ]
    },
...]
```

Fetch all bikes filtered on city and zone type:

Requires admin token.

>GET /bikes?city=\<city>&zone_type=\<zone type>

```javascript
const token = localStorage.getItem('token');

const response = await fetch('/api/v1/bikes?city=karlskrona&zone_type=charging', {
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
        "bike_id": 1505,
        "city": "Karlskrona",
        "status": "charging",
        "coordinates": {
            "type": "Point",
            "coordinates": [
                15.585025499346187,
                56.166004837144186
            ]
        },
        "zones": [
            {
                "zone_id": 48,
                "zone_type": "charging"
            }
        ]
    },
    {
        "bike_id": 1566,
        "city": "Karlskrona",
        "status": "charging",
        "coordinates": {
            "type": "Point",
            "coordinates": [
                15.587385940998042,
                56.15851613289694
            ]
        },
        "zones": [
            {
                "zone_id": 46,
                "zone_type": "charging"
            }
        ]
    },
    {
        "bike_id": 1567,
        "city": "Karlskrona",
        "status": "charging",
        "coordinates": {
            "type": "Point",
            "coordinates": [
                15.587374915908704,
                56.15855634665777
            ]
        },
        "zones": [
            {
                "zone_id": 46,
                "zone_type": "charging"
            }
        ]
    },
    {
        "bike_id": 1568,
        "city": "Karlskrona",
        "status": "charging",
        "coordinates": {
            "type": "Point",
            "coordinates": [
                15.587381155396795,
                56.15853145354702
            ]
        },
        "zones": [
            {
                "zone_id": 46,
                "zone_type": "charging"
            }
        ]
    },
...]
```

Fetch all bikes filtered on city and status:

Third parties and customers may filter on status available, all other filters require an admin token.

>GET /bikes?city=\<city>&status=\<status>
```javascript
const token = localStorage.getItem('token');

const response = await fetch('/api/v1/bikes?city=umeå&status=available', {
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
[
    {
        "bike_id": 1026,
        "city": "Umeå",
        "status": "available",
        "coordinates": {
            "type": "Point",
            "coordinates": [
                20.260739715844622,
                63.827344171716085
            ]
        },
        "zones": [
            {
                "zone_id": 50,
                "zone_type": "city"
            },
            {
                "zone_id": 51,
                "zone_type": "slow"
            },
            {
                "zone_id": 52,
                "zone_type": "parking"
            }
        ]
    },
    {
        "bike_id": 1027,
        "city": "Umeå",
        "status": "available",
        "coordinates": {
            "type": "Point",
            "coordinates": [
                20.2607516078436,
                63.827322307867284
            ]
        },
        "zones": [
            {
                "zone_id": 50,
                "zone_type": "city"
            },
            {
                "zone_id": 51,
                "zone_type": "slow"
            },
            {
                "zone_id": 52,
                "zone_type": "parking"
            }
        ]
    },
...]
```
Update bike status:

>PUT /bikes/:id

Required parameters:

>bike_id<br>

```javascript
const bike = { status: "deleted" };
const response = await fetch(`/api/v1/bikes/:id`, {
    method: 'PUT',
    headers: {
    'Authorization': `Bearer ${token}`,
    'Content-Type': 'application/json'
    },
    body: JSON.stringify(bike)
    });
```

Result:

```json
{
    "success": true,
    "message": "Status updated"
}
```
