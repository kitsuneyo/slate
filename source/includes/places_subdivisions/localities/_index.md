## Subdivision localities: get all

> HTTP 200 response body

```JSON
{
  "data": [
    {
      "id": "2894",
      "type": "place_localities",
      "attributes": {
        "slug": "austin-texas-united-states",
        "name": "Austin",
        "formatted": "Austin, Texas, United States",
        "also_known_as": [],
        "latitude": null,
        "longitude": null
      },
      "relationships": {
        "created_by": {
          "data": {
            "id": "1",
            "type": "users"
          },
          "links": {
            "related": "http://api.dbljump.com/users/1"
          }
        },
        "country": {
          "data": {
            "id": "220",
            "type": "place_countries"
          },
          "links": {
            "related": "http://api.dbljump.com/places/countries/united-states"
          }
        },
        "subdivision": {
          "data": {
            "id": "2599",
            "type": "place_subdivisions"
          },
          "links": {
            "related": "http://api.dbljump.com/places/subdivisions/texas-united-states"
          }
        }
      },
      "links": {
        "self": "http://api.dbljump.com/places/localities/austin-texas-united-states"
      }
    }
  ],
  "links": {},
  "meta": {
    "total_items": 1
  }
}
```

Retrieve all localities belonging to the given subdivision. Automatically paginated.

* User authentication: not required
* Authorization level: n/a

### HTTP request

`GET /places/subdivisions/{subdivision-slug}/localities` (replace `{subdivision-slug}` with subdivision record slug)

### URL query parameters

Parameter | Default | Description
--------- | ------- | -----------
page[number] | 1 | Select the page number
page[size] | 30 | Select the number of images per page

### Success HTTP response code

`200 OK`