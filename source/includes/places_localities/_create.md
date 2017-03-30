## <a name="localities_create"></a>Create a new locality record

> Request body

```JSON
{
  "data": {
    "type": "place_localities",
    "attributes": {
      "subdivision_id": "1000",
      "name": "New City",
      "also_known_as": ["That New City", "The New Locality"],
      "latitude": "81.3",
      "longitude": "-45.9"
    }
  }
}
```

> HTTP 201 response body

```JSON
{
  "data": {
    "id": "2939",
    "type": "place_localities",
    "attributes": {
      "name": "New City",
      "formatted": "New City, Enugu, Nigeria",
      "also_known_as": [
        "That New City",
        "The New Locality"
      ],
      "latitude": 81.3,
      "longitude": -45.9
    },
    "relationships": {
      "subdivision": {
        "data": {
          "id": "1000",
          "type": "place_subdivisions"
        }
      },
      "created_by": {
        "data": {
          "id": "3",
          "type": "users"
        }
      }
    },
    "links": {
      "self": "http://api.dbljump.com/places/localities/new-city-enugu-nigeria",
      "subdivision": "http://api.dbljump.com/places/subdivisions/enugu-nigeria",
      "country": "http://api.dbljump.com/places/countries/nigeria"
    }
  }
}
```

Create a new locality record. Admin-level authorization required.

* User authentication: required
* Authorization level: admin

### HTTP request

`POST /places/localities`

### Request attributes

Attribute | Type | Req'd? | Description
--------- | ---- | ------ | -----------
subdivision_id | integer | Y | ID of parent subdivision.
name | string | Y | 2-250 chars. English-language common name, e.g. 'Los Angeles'.
also_known_as | array | | Members must be 2-50 char strings. E.g. `['LA', 'City of Angels']`.
latitude | number/float | | Between -90 and 90.
longitude | number/float | | Between -180 and 180.

### Success HTTP response code

`201 Created`