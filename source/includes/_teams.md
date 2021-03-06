# Teams

A Team in Upwave is a container for Boards.


## View a Team

`GET https://api.upwave.io/workspaces/1337/teams/482/`

```shell
curl "https://api.upwave.io/workspaces/1337/teams/482/"
  -H "Authorization: Token 9944b09199c62bcf9418ad846dd0e4bbdfc6ee4b"
```

> The above command returns JSON structured like this:

```json
{
    "id": 482,
    "title": "R & D",
    "hex_color": "#00796b",
    "hex_text_color": "#ffffff",
    "access":{
        "can_admin": true,
        "can_modify": true,
        "can_invite": true,
        "can_invite_existing": true
    }
}
```


## List Teams

`GET https://api.upwave.io/workspaces/1337/teams/`

```shell
curl "https://api.upwave.io/workspaces/1337/teams/"
  -H "Authorization: Token 9944b09199c62bcf9418ad846dd0e4bbdfc6ee4b"
```

> The above command returns JSON structured like this:

```json
{
    "count": 1,
    "next": null,
    "previous": null,
    "results": [
        {
            "id": 482,
            "title": "R & D",
            "access":{
                "can_admin": true,
                "can_modify": true,
                "can_invite": true,
                "can_invite_existing": true
            }
        }
    ]
}
```
