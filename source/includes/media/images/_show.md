## <a name="images_show"></a>Get single image

> Response body | `HTTP 200`

```JSON
# GET /media/images/mario-figure-photo

{
  "data": {
    "id": "2",
    "type": "images",
    "attributes": {
      "kind": "photo",
      "slug": "mario-figure-photo",
      "original": "https://dbljumpheroku.s3.amazonaws.com/uploads/images/2/mario-figure.jpg",
      "thumb": "https://dbljumpheroku.s3.amazonaws.com/uploads/images/2/th_mario-figure.jpg",
      "title": "Mario figure",
      "description": "",
      "year": 2016,
      "date": "2016-07-30",
      "usage_type": "free",
      "usage_license_code": null,
      "usage_license_name": null,
      "usage_license_url": null,
      "attributed_name": null,
      "attributed_url": null,
      "source_url": ""
    },
    "relationships": {
      "uploaded_by": {
        "data": {
          "id": "1",
          "type": "users"
        },
        "links": {
          "related": "http://api.dbljump.com/users/1"
        }
      },
      "place": {
        "data": null,
        "links": {
          "related": "http://api.dbljump.com/places/afghanistan"
        }
      }
    },
    "links": {
      "self": "http://api.dbljump.com/media/images/mario-figure-photo"
    }
  },
  "included": [
    {
      "id": "1",
      "type": "users",
      "attributes": {
        "username": "tikithekiwi",
        "role": "admin",
        "given_names": "Tiki",
        "family_name": "the Kiwi",
        "avatar": null
      },
      "links": {
        "self": "http://api.dbljump.com/users/1"
      }
    }
  ],
  "meta": {
    "keywords": "mario figure, photo, 2016, 2016-07-30, image, picture, media, dbljump, video games, pc games, gaming",
    "description": "'Mario figure' is a video game image at Dbljump.",
    "created_at": "2017-04-21T09:27:48.640Z",
    "updated_at": "2017-04-21T09:27:48.640Z"
  }
}
```

Retrieve a single image record. Images are publicly available. No sign-in is required.

* User authentication: not required
* Authorization level: n/a

### HTTP request

`GET /media/images/{slug}` (replace `{slug}` with image record slug)

### Success HTTP response code

`200 OK`

### <a name="image_response_attrs"></a>Response attributes

Attribute | Type | Req'd? | Description
--------- | ---- | ------ | -----------
original | string | Y | URL of the original file.
thumb | string | Y | URL of the thumbnail version, resized to max-width 300px.
slug | string | Y | A record ID based on metadata, e.g. 'photo-of-hideo-kojima'.
kind | string | Y | See [Kind](#image_kind).
title | string | Y | The image title.
description | string | | The image description.
year | integer | | Year the image was created.
date | date | | Date the image was created.
usage_type | string | Y | One of three usage types:'free', 'fair', or 'licensed'. See [Usage type](#image_usage_type).
usage_license_code | string | * | Req'd if usage_type is 'licensed'. See [Usage license](#image_usage_license) section.
attributed_name | string | * | The image owner's name. Always present if usage_type is 'licensed'.
attributed_url | string | | The image owner's website URL.
source_url | string | * | The URL the image was sourced from. Always present if usage_type is 'licensed'.

### Relationships

Association | Record type | Relationship type
------------ | ---------- | -----------------
uploaded_by | users | belongs_to |
place | places | belongs_to

### Meta

The `meta` section of the JSON response includes `keywords`, `description`, `created_at` and `updated_at` attributes.
