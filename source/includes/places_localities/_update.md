## <a name="localities_update"></a>Update a locality record

> Request body

```JSON
{
  "data": {
    "type": "place_localities",
    "id": "matsumoto-nagano-prefecture-japan",
    "attributes": {
      "subdivision_id": "1001",
      "name": "Updated City",
      "also_known_as": ["Updated City", "Changed Locality"],
      "latitude": "24.0",
      "longitude": "89.5"
    }
  }
}
```

> HTTP 200 response body

```JSON
{
  "data": {
    "id": "2936",
    "type": "place_localities",
    "attributes": {
      "name": "Updated City",
      "formatted": "Updated City, Epirus, Greece",
      "also_known_as": [
        "Updated City",
        "Changed Locality"
      ],
      "latitude": 24,
      "longitude": 89.5
    },
    "relationships": {
      "subdivision": {
        "data": {
          "id": "1001",
          "type": "place_subdivisions"
        }
      },
      "created_by": {
        "data": {
          "id": "1",
          "type": "users"
        }
      }
    },
    "links": {
      "self": "http://api.dbljump.com/places/localities/updated-city-epirus-greece",
      "subdivision": "http://api.dbljump.com/places/subdivisions/epirus-greece",
      "country": "http://api.dbljump.com/places/countries/greece"
    }
  }
}
```

Update an existing locality record. The user must be an admin.

* User authentication: required
* Authorization level: admin

### HTTP request

`PATCH /places/localities/{slug}` (replace `{slug}` with locality record slug)

### Request attributes

Attribute | Type | Description
--------- | ---- | -----------
subdivision_id | integer | Y | ID of parent subdivision.
name | string | Y | 2-250 chars. English-language common name, e.g. 'Los Angeles'.
also_known_as | array | | Members must be 2-50 char strings. E.g. `['LA', 'City of Angels']`.
latitude | number/float | | Between -90 and 90.
longitude | number/float | | Between -180 and 180.

### Success HTTP response code

`200 OK`