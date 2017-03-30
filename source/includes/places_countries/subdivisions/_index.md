## Country subdivisions: get all

> HTTP 200 response body

```JSON
{
  "data": [
    {
      "id": "504",
      "type": "place_subdivisions",
      "attributes": {
        "name": "Australian Capital Territory",
        "formatted": "Australian Capital Territory, Australia",
        "latitude": -35.4734679,
        "longitude": 149.0123679,
        "also_known_as": []
      },
      "relationships": {
        "created_by": {
          "data": {
            "id": "1",
            "type": "users"
          },
          "links": {
            "related": "http://localhost:3000/users/1"
          }
        },
        "country": {
          "data": {
            "id": "12",
            "type": "place_countries"
          },
          "links": {
            "related": "http://localhost:3000/places/countries/australia"
          }
        },
        "localities": {
          "data": []
        }
      },
      "links": {
        "self": "http://localhost:3000/places/subdivisions/australian-capital-territory-australia"
      }
    },
    {
      "id": "815",
      "type": "place_subdivisions",
      "attributes": {
        "name": "Christmas Island",
        "formatted": "Christmas Island, Australia",
        "latitude": null,
        "longitude": null,
        "also_known_as": []
      },
      "relationships": {
        "created_by": {
          "data": {
            "id": "1",
            "type": "users"
          },
          "links": {
            "related": "http://localhost:3000/users/1"
          }
        },
        "country": {
          "data": {
            "id": "12",
            "type": "place_countries"
          },
          "links": {
            "related": "http://localhost:3000/places/countries/australia"
          }
        },
        "localities": {
          "data": []
        }
      },
      "links": {
        "self": "http://localhost:3000/places/subdivisions/christmas-island-australia"
      }
    },
    {
      "id": "834",
      "type": "place_subdivisions",
      "attributes": {
        "name": "Cocos (Keeling) Islands",
        "formatted": "Cocos (Keeling) Islands, Australia",
        "latitude": null,
        "longitude": null,
        "also_known_as": []
      },
      "relationships": {
        "created_by": {
          "data": {
            "id": "1",
            "type": "users"
          },
          "links": {
            "related": "http://localhost:3000/users/1"
          }
        },
        "country": {
          "data": {
            "id": "12",
            "type": "place_countries"
          },
          "links": {
            "related": "http://localhost:3000/places/countries/australia"
          }
        },
        "localities": {
          "data": []
        }
      },
      "links": {
        "self": "http://localhost:3000/places/subdivisions/cocos-keeling-islands-australia"
      }
    }
  ],
  "links": {},
  "meta": {
    "total_items": 13
  }
}
```

Retrieve all subdivisions belonging to the given country. Automatically paginated.

* User authentication: not required
* Authorization level: n/a

### HTTP request

`GET /places/countries/{country-slug}/subdivisions` (replace `{country-slug}` with country record slug)

### URL query parameters

Parameter | Default | Description
--------- | ------- | -----------
page[number] | 1 | Select the page number
page[size] | 30 | Select the number of images per page

### Success HTTP response code

`200 OK`