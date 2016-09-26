---
title: Smart Fridge

language_tabs:
  - json


toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

This api is the thing thing ding.
# Authentication

> To authorize, send the UserId with every request:

<aside class="notice">
All parameters are send in the POST variable JSON.
</aside>
Parameter | Default | Description
--------- | ------- | -----------
UserId | -- |




```json
	{"UserId": "jfujasdfdoiasdfpasdfoip",
	...
	}
```

> Make sure to replace `meowmeowmeow` with your API key.

Kittn uses API keys to allow access to the API. You can register a new Kittn API key at our [developer portal](http://example.com/developers).

Kittn expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: meowmeowmeow`

<aside class="notice">
You must replace <code>meowmeowmeow</code> with your personal API key.
</aside>

# Contains


```json
{
"UserId":"asdfasdf",
(optional)
"Sort" : "opened+closed/everything/opened/closed"
}
```
>The everything command returns also the items that were in the fridge. now no things

```json
[
  {
    "id": 1,
    "name": "1kg brown sugar",
    "barcode": "10293838128182891212",
    "closed": 4,
    "opened": 1
  },
  {
    "id": 2,
    "name": "Monster beer",
    "barcode": "091991290913213",
    "closed": 5,
    "opened": 10
  }
  ...
]
```

This gets all the items in the fridge, opened and closed.

### HTTP Request

`POST /api/contains`

### Query Parameters

Parameter | Default | Possible values | Description	|
--------- | ------- | --------------- |  -----------
(OPTIONAL)Sort | opened+closed | everything/opened/opened+closed/closed | Get the type of items in the fridge.


# Get Jobs
The jobs are the things that the fridge has to do, from printing a barcode to playing a song(not implemented :P)

```json
{
"UserId":"asdfasdfsadf",
(optional)
"Status":"new/all/done",
"Type": "all/qrCode/text/list/restart/halt/"
}
 ```
>The JSON output, an array of (different sorts)

```json
{
[{
"Type":"qrCode",
"Code": "9120398890",
"Status":"new/done",
"JobId":82712
},
{
"Type":"text" ,
"Text":"This will be printed by the fridge",
"Status":"new/done",
"JobId":82733
},
{
"Type": "list",
"Items":[
		{"Title":"1kg apples"},
		{"Title":"Big pack milk"}],
"Status":"new/done",
"JobId":82733
}
]
}
```



### HTTP Request

`POST /api/getJobs`

### Query Parameters

Parameter | Default | Possible values | Description	|
--------- | ------- | --------------- |  -----------
(OPTIONAL)Status | new | new/all/done | Get only the jobs of with that status
(OPTIONAL)Type  | all | all/qrCode/text/list/reboot/halt/etc.... | Get only the jobs of that type

# Mark jobs


```json
"userId": "asdfasdfasdf",
"JobId":12345,
(Optional)
"Status":"done/new"}
```
>Or in an array:
```json
{"userId": "asdfasdfasdf",
"Jobs":[
  {"JobId":12345,
    (Optional)
  "Status": "done/new"},
  {"JobId":12346,
    (Optional)
  "Status": "done/new"}

  ]}
```
>The output
```json
{"JobId":12345,
"Status":"done/new"}
```
>Or in an array:
```json
{"Jobs":[{"JobId":12345,
"Status":"done/new"},
{"JobId":12346,
"Status":"done/new"}
]}
```

This gets all the items in the fridge, opened and closed.

### HTTP Request

`POST /api/contains`

### Query Parameters

Parameter | Default | Possible values | Description	|
--------- | ------- | --------------- |  -----------
(OPTIONAL)Sort | opened+closed | everything/opened/opened+closed/closed | Get the type of items in the fridge.



#mark Jobs
Mark the jobs done or new.asdf This way the Fridge won't print unlimited barcodes or other things.
```json
{"userId": "asdfasdfasdf",
"JobId":12345,
(Optional)
"Status":"done/new"}```
>Or in an array:
```json
{"userId": "asdfasdfasdf",
"Jobs":[
  {"JobId":12345,
    (Optional)
  "Status": "done/new"},
  {"JobId":12346,
    (Optional)
  "Status": "done/new"}

  ]}
```

>The output
```json
{"JobId":12345,
"Status":"done/new"}
```
>Or in an array:
```json
{"Jobs":[{"JobId":12345,
"Status":"done/new"},
{"JobId":12346,
"Status":"done/new"}
]}
```
###Http request
'POST /api/markJob'


























lel
