## Get all of a company's child kinships

> Response body | `HTTP 200`

```JSON
# GET /articles/companies/nintendo-co-ltd/children

{
    "data": [
        {
            "id": "1",
            "type": "company_kinships",
            "attributes": {
                "kind": "division",
                "start_year": null,
                "end_year": null
            },
            "relationships": {
                "parent": {
                    "data": {
                        "id": "1",
                        "type": "companies"
                    },
                    "links": {
                        "related": "http://localhost:3000/articles/companies/nintendo-co-ltd"
                    }
                },
                "child": {
                    "data": {
                        "id": "5",
                        "type": "companies"
                    },
                    "links": {
                        "related": "http://localhost:3000/articles/companies/nintendo-entertainment-analysis-development"
                    }
                }
            }
        },
        {
            "id": "2",
            "type": "company_kinships",
            "attributes": {
                "kind": "division",
                "start_year": null,
                "end_year": null
            },
            "relationships": {
                "parent": {
                    "data": {
                        "id": "1",
                        "type": "companies"
                    },
                    "links": {
                        "related": "http://localhost:3000/articles/companies/nintendo-co-ltd"
                    }
                },
                "child": {
                    "data": {
                        "id": "22",
                        "type": "companies"
                    },
                    "links": {
                        "related": "http://localhost:3000/articles/companies/retro-studios-inc"
                    }
                }
            }
        },
        {
            "id": "3",
            "type": "company_kinships",
            "attributes": {
                "kind": "ownership",
                "start_year": null,
                "end_year": null
            },
            "relationships": {
                "parent": {
                    "data": {
                        "id": "1",
                        "type": "companies"
                    },
                    "links": {
                        "related": "http://localhost:3000/articles/companies/nintendo-co-ltd"
                    }
                },
                "child": {
                    "data": {
                        "id": "21",
                        "type": "companies"
                    },
                    "links": {
                        "related": "http://localhost:3000/articles/companies/monolith-soft-inc"
                    }
                }
            }
        }
    ],
    "links": {},
    "meta": {
        "total_items": 3
    }
}
```

Retrieve all of a given company's child kinships. Automatically paginated.

* User authentication: not required
* Authorization level: n/a

### HTTP request

`GET /articles/companies/{company-slug}/children` (replace `{company-slug}` with company record slug)

### URL query parameters

Parameter | Default | Description
--------- | ------- | -----------
fields[{record-type}] | All fields | Return only specified fields, e.g. `?fields[company_kinships]=kind`
filter[{field}] | All records | Filter search by field, e.g. `?filter[kind]=division`
page[number] | 1 | Select the page number, e.g. `?page[number]=3`
page[size] | 30 | Select the number of records per page, e.g. `?page[size]=20`

### Success HTTP response code

`200 OK`