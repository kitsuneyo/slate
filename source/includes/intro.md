# Introduction

The Dbljump API is a system for cataloging and serving data about video games and the video game industry.

It is part of a wider group of software, Dbljump, which is made up of:

* The Dbljump [PostgreSQL](https://www.postgresql.org) database
* The back-end dbljump/rails-api, a [Ruby on Rails](http://rubyonrails.org) application that manages the database and provides the API described here. This is currently under development.
* The front-end client dbljump/client-ember, an [Ember.js](https://www.emberjs.com) application that provides a web user interface. This is currently under development.
* [Dbljump.com](http://www.dbljump.com), the web domain where it all comes together

This API is therefore designed to be used exclusively by the Dbljump front-end client.

This documentation, which describes the features of the API and how to use them, is intended for use by the Dbljump development team. It was built with [Slate](https://github.com/lord/slate) and is hosted with [GitHub Pages](https://pages.github.com).

**For more information, or if you want to contribute or join us, please visit [www.dbljump.com](http://www.dbljump.com).**

## How to use

Basic rules for making API requests.

### Domain

URLs in this documentation exclude the domain where the production API is hosted. Prepend the current domain name to URLs when making requests, e.g. `http://api.dbljump.com/articles/games`.

### JSON API specification

This API accepts and returns JSON data, following the JSON API specification as closely as possible.

[Read more about the specification](http://jsonapi.org).

### HTTP headers: request content-type and version

In accordance with the JSON API spec, all requests must include two HTTP headers, which declare the content-type and API version number:

* `Accept:application/vnd.api+json; version={vnum}`
* `Content-Type:application/vnd.api+json; version={vnum}`

Replace `{vnum}` with the API version number you want to use. The current version number is `1`, and this is not expected to change anytime soon!

### HTTP headers: response content-type

Successful responses include the following HTTP header:

* `Content-Type:application/vnd.api+json; charset=utf-8`

## Authorizing requests and logging in users

Many Dbljump API requests require authorization. This API uses JWTs for authentication and authorization, instead of HTTP sessions. When authorization is needed, it must be provided via a [JSON web token (JWT)](https://jwt.io) included in the `Authorization` HTTP header.

The presence and [payload content](#the-jwt-payload) of a JWT determines:

* whether or not a user is 'logged in'
* the authorization level of the user identified by the JWT
* whether the request is authorized (based on the validity of the JWT and the user's authorization level)

### HTTP headers: request authorizations

A valid `Authorization` header and JWT must always be _included_ when the client user is logged in and always _excluded_ when the client user is not logged in.

The header must be provided as follows:

* `Authorization:Bearer {user-jwt}`

Replace `{user-jwt}` with a JWT returned by a successful [user authentication request](#users-authentications).

### The JWT payload

As well providing request authorization, JWTs contain a JSON payload the client can decode and use to identify the logged-in user.

JWT payload attribute | Description
--------------------- | -----------
`user_id` | Can be used to [get the logged-in user's record](#get-single-user).
`user_role` | Determines the user's authorization level. Can be `member`, `editor` or `admin`.
`expiry` | The JWT expiry date and time.

### User role and authorization level

API request authorization also depends on the `role` of the user that the passed JWT belongs to.

Users can have one of three roles:

Role                | Description
------------------- | -----------
`member`            | Ordinary user. Can sign in and view pages but has very limited abilities.
`editor`            | Can create, edit (and in some cases delete) articles and images.
`admin`             | Can do everthing, including managing users, places, platform, genres and so on.

This documentation describes the authorization level required to use each each API feature.

## Using URL queries

> URL query examples

```
# Include all primary_image items related to articles in the response:
/articles/games?include=primary_image

# Specify sparse fieldsets for users and images (users are included by
# default):
/users/2/images?fields[users]=username,avatar&fields[images]=title,thumb

# Use filter to only return items where kind == 'photo':
/media/images?filter[kind]=photo

# Specify 10 items per page and return page 5:
/users?page[size]=10&page[number]=5

# Sort by two fields: kind (ascending) and created_by_id (descending
# as prepended by a dash):
/media/images?sort=kind,-created_by_id

# Search for platforms related to 'nintendo'
/platforms?search=nintendo
```

This API supports URL queries, including those [specified by JSON API](http://jsonapi.org/format/#fetching):

Query             | Description
----------------- | -----------
`fields[{type}]`  | Specify sparse fieldsets. You must provide the type(s) and field name(s).
`filter[{field}]` | Filter data by a given field and value.
`include[{type}]` | Include resources related to the main dataset.
`page[size]`      | Specify how many items should be on each page. Defaults to `30`.
`page[number]`    | Specify the page number. Defaults to `1`.
`search`          | Use with `GET` collection endpoints. Search by string.
`sort`            | Sort the data by specified fields. Prepend the field name with a `-` to sort descending.

### Filter fields

Below is a table of fields by which you can filter each record-type.

Record type | Filterable fields
----------- | ---------------
articles    | type, kind, origin_date, origin_year, origin_place_id, ended, end_date, end_year, latest_place_id, status, created_by_id, last_review_outcome, last_reviewed_by_id, published_at
genres      | created_by_id
places      | kind, parent_id, created_by_id
platforms   | holder_id, sphere, kind, parent_id, created_by_id
users       | gender, role, birthday, country_id, activated_at
credits     | credited_id, game_id, version_id, place_id, role, category
kinships    | parent_id, child_id, kind, start_year, end_year
names       | article_id, version_id, name_or_title, family_name, given_names, kind, writing_system, year_adopted, year_dropped, dropped
notes       | article_id, version_id, type, category, cite_website, created_by_id
images      | kind, year, date, place_id, uploaded_by_id, usage_type, usage_license_code, attributed_name
versions    | game_id, platform_id, status, fps_target, fps_unlocked, res_w, res_h, res_unlocked
releases    | version_id, place_id, date, year, physical, digital

### Searchable record types

Below is a list of record types that accept search queries.

* `companies`
* `games`
* `genres`
* `images`
* `people`
* `places`
* `platforms`
* `users`

### Sort fields

Below is a table of fields by which you can sort each record-type.

Record type | Sortable fields
----------- | ---------------
articles    | type, sort_title, origin_date, origin_year, created_by_id, status, last_submitted_at, last_reviewed_at, last_review_outcome, published_at
genres      | name, short_name, parent_id, created_by_id
places      | name, formatted, type, kind, parent_id, created_by_id, iso_code
platforms   | holder_id, name, short_name, sphere, kind, parent_id, created_by_id
users       | email, family_name, gender, username, role, birthday, country_id, last_signed_in_at, sign_in_count, activation_sent_at, activated_at, password_reset_sent_at
credits     | credited_id, game_id, version_id, place_id, role, category
kinships    | kind, start_year, end_year
names       | name_or_title, family_name, given_names, kind, writing_system, year_adopted, year_dropped, dropped
notes       | type, category, cite_website, created_by_id
images      | kind, title, year, date, place_id, uploaded_by_id, usage_type
versions    | game_id, platform_id, status, fps_target, fps_unlocked, res_w, res_h, res_unlocked
releases    | version_id, place_id, date, year, physical, digital
