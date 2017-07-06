# Cards

UpWave Cards are information carriers that can hold task-description, comments, files etc.

### Watching a Card

A User, when on a watch list to a Card, will be notified on important changes on that Card.
The user will automatically be added to the watch list when..
a) the user is assigned a Card,
b) the user is mentioned in a Comment on a Card
c) the user choose to watch the Card

The only way to unwatch is to update the card with *{"watch": false}*
This is also the mechanism for how to manually add oneselves to the watch list.

## List Cards

`GET https://<TEAM DOMAIN>.upwave.io/api/cards/`

```shell
curl "https://<TEAM DOMAIN>.upwave.io/api/cards/"
  -H "Authorization: <API TOKEN>"
```

> The above command returns JSON structured like this:

```json
  {
    "count": 7, 
    "next": "https://<TEAM DOMAIN>.upwave.io/api/cards/?page=2",
    "previous": None, 
    "results": [
      {
        "id": 4723,
        "title": "A Card",
        "description": "<h1>A Card</h1><p>More text in a paragraph.</p>",
        "color": null,
        "created_dt": "2016-07-13T10:33:26.645Z",
        "created_by_user": {
          "id": 2,
          "email": "person2@example.com",
          "fullname": "Lisa Doe",
          "firstname": "Lisa",
          "avatar": "https://my.profile.image"
        },
        "finished_dt": "2016-08-04T08:53:24.921Z",
        "due_dt": null,
        "assigned": [
          {
            "id": 1,
            "email": "person1@example.com",
            "fullname": "John Doe",
            "firstname": "John",
            "avatar": "https://my.profile.image"
          },
          {
            "id": 2,
            "email": "person2@example.com",
            "fullname": "Lisa Doe",
            "firstname": "Lisa",
            "avatar": "https://my.profile.image"
          },
        ]
      },
      ..
    ]
  }
```

This endpoint retrieves all the Cards you can access in a paginated fashion.
They are ordered by creation date (created_dt) with the newest Card listed first.

### Filters

Parameter | Format | Description
--------- | ------- | ---- | -----------
created_by_user | `integer` | Filter Cards on what user created them
created_start | `YYYY-MM-DD` | Filter Cards that were created on or after this date
created_end | `YYYY-MM-DD` | Filter Cards that were created on or before this date
due_start | `YYYY-MM-DD` | Filter Cards that have due_dt on or after this date
due_end | `YYYY-MM-DD` | Filter Cards that have due_dt on or before this date
finished_start | `YYYY-MM-DD` | Filter Cards that were completed on or after this date
finished_end | `YYYY-MM-DD` | Filter Cards that were completed on or before this date
finished | `true/false` | Filter Cards on whether they are completed or not
state | `integer` | Filter Cards based on their column state
board | `integer` | Filter Cards based on their parent Board
assigned | `1,2,3` | Filter Cards based on who are assigned
q | `querystring` | Search for querystring in Card title and description
ordering | `field` | Order result-set by field (default "-created")
page_size | `integer` | Size of result-set per page

The `assigned` parameter supports comma separated list which will be OR'ed.
For example, to filter Cards that are assigned to either of user-account 1 or 2 you can pass in:
`?assigned=1,2`

The ordering parameter will order the result-set on the field given. Acceptable fields are:
"created", "finished", "due". To specify a descending ordering direction set a minus in front e.g. `?ordering=-created`

When filters are combined they will be AND'ed together. For example to list all Cards that were 
completed in month July 2017, combine filters like so: `?finished_start=2017-07-1&finished_end=2017-07-31`

## Get a Specific Card

`GET https://<TEAM DOMAIN>.upwave.io/api/cards/<ID>/`

This endpoint retrieves a specific Card.

```shell
curl "https://<TEAM DOMAIN>.upwave.io/api/cards/4723/"
  -H "Authorization: <API TOKEN>"
```

> The above command returns JSON structured like this:

```json
  {
    "id": 4723,
    "title": "A Card",
    "description": "<h1>A Card</h1><p>More text in a paragraph.</p>",
    "color": null,
    "created_dt": "2016-07-13T10:33:26.645Z",
    "created_by_user": {
      "id": 2,
      "email": "person2@example.com",
      "fullname": "Lisa Doe",
      "firstname": "Lisa",
      "avatar": "https://my.profile.image"
    },
    "finished_dt": "2016-08-04T08:53:24.921Z",
    "due_dt": null,
    "assigned": [
      {
        "id": 1,
        "email": "person1@example.com",
        "fullname": "John Doe",
        "firstname": "John",
        "avatar": "https://my.profile.image"
      },
      {
        "id": 2,
        "email": "person2@example.com",
        "fullname": "Lisa Doe",
        "firstname": "Lisa",
        "avatar": "https://my.profile.image"
      },
    ],
    "watched": true
  }
```

In order to fetch additional data belonging to a Card, such as Comments, Attachments, TaskListItems,
use the appropriate API with a card-filter. Example: *api/comments/?card=\<CARD ID\>*