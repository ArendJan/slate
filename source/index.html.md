---
title: Smart Fridge

language_tabs:
  - json


toc_footers:
  - <a href='http://pws.svshizzle.com/'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/tripit/slate'>Documentation Powered by Slate</a>


search: true
---

# Introduction

This api for the Smartfridge Project made by Arend-Jan van Hilten & Vincent Kling. Please go to [our website](http://pws.svshizzle.com). to view it in action and go to [hackster.io](https://www.hackster.io/ajv/smart-fridge-4a50b5) to make it yourself.
# Authentication

> To authorize, send the UserId with every request:

<aside class="notice">
All parameters are send in the POST variable JSON.
</aside>
Parameter | Default | Description
--------- | ------- | -----------
UserId | -- | Your own userId




```json
	{"UserId": "oesereideah",
	...
	}
```

> Make sure to replace `oesereideah` with your API key.


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
    "Id": 1,
    "Name": "1kg brown sugar",
    "Barcode": "10293838128182891212",
    "Closed": 4,
    "Open": 1
  },
  {
    "Id": 2,
    "Name": "Monster beer",
    "Barcode": "091991290913213",
    "Closed": 5,
    "Open": 10
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
"Type": "all/barcode/text/list/restart/halt/"
}
 ```
>The JSON output, an array of (different sorts)

```json
{
[{
"Type":"barcode",
"Code": "9120398890",
"Status":"new/done",
"JobId":"82712"
},
{
"Type":"text" ,
"Text":"This will be printed by the fridge",
"Status":"new/done",
"JobId":"82733"
},
{
"Type": "list",
"Items":[
		{"Title":"1kg apples"},
		{"Title":"Big pack milk"}],
"Status":"new/done",
"JobId":"82733"
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
(OPTIONAL)Type  | all | all/barcode/text/list/reboot/halt/etc.... | Get only the jobs of that type

# Mark Jobs


```json
{"UserId": "asdfasdfasdf",
"JobId":"12345",
(Optional)
"Status":"done/new"}
```

>Or in an array:


```json
{"UserId": "asdfasdfasdf",
"Jobs":[
  {"JobId":"12345",
    (Optional)
  "Status": "done/new"},
  {"JobId":"12346",
    (Optional)
  "Status": "done/new"}

  ]}
```

>The output

```json
{"JobId":"12345",
"Status":"done/new"}
```

>Or in an array:

```json
{"Jobs":[{"JobId":"12345",
"Status":"done/new"},
{"JobId":"12346",
"Status":"done/new"}
]}
```

Mark the jobs done or new.asdf This way the Fridge won't print unlimited barcodes or other things.


### HTTP Request

`POST /api/markJob`

### Query Parameters

Parameter | Default | Possible values | Description	|
--------- | ------- | --------------- |  -----------
JobId | - | - | The id of the job. This id is unique and will be given via the getJobs request. String because PHP is weird...
Status | done | done/new | The new status of the job.
(OPTIONAL)Sort | opened+closed | everything/opened/opened+closed/closed | Get the type of items in the fridge.


#Add Job

This will create a new job.

### HTTP Request

`POST /api/addJob`

##Text
Create a job that will print a text.

```json
{"UserId": "asdfasdfasdf",
"Type": "Text",
"Text": "The text of your choise."}
```

>Will output:

```json
{"JobId": 12345}
```

###Query Parameters
Parameter | Default | Possible values | Description	|
--------- | ------- | --------------- |  -----------
Type | - | - | The type of the new job. You can add new types. See down.
Text | - | - | The text that will be printed.

##Barcode
Create a job that will print a new barcode for a new item.
The Code variable is a String, because of server reasons. Needs to be EAN13.

```json
{"UserId": "asdfasdfasdf",
"Type": "barcode",
"Code": "11234567891011"}
```

>Output the same as text

###Query Parameters

Parameter | Default | Possible values | Description	|
--------- | ------- | --------------- |  -----------
Type | barcode | - | print the barcode.
Code | -| - | The barcode you want to print. The Code variable is a String, because of server reasons. Needs to be EAN13.


##Shut down
Create a job that will shut down the Raspberry Pi, by sending sudo halt to the terminal.

```json
{"UserId": "asdfasdfasdf",
"Type": "shutdown"}
```

>Output the same as text

###Query Parameters

Parameter | Default | Possible values | Description	|
--------- | ------- | --------------- |  -----------
Type | shutdown | - | easy and fast.

##Reboot
Create a job that will restart the Raspberry Pi. This is usefull when there is new software. Sends sudo reboot to the terminal

```json
{"UserId": "asdfasdfasdf",
"Type": "reboot"
}
```

>Output the same as text

###Query Parameters

Parameter | Default | Possible values | Description	|
--------- | ------- | --------------- |  -----------
Type | reboot | - | GG EZ


##Update
Create a job that will update the smartfridge software by downloading the new software, installing it(putting it in the right place), and restarting the software.

```json
{"UserId": "asdfasdfasdf",
"Type": "update"
}
```

>Output the same as text

###Query Parameters

Parameter | Default | Possible values | Description	|
--------- | ------- | --------------- |  -----------
Type | update | - | Downloads from the master and will delete every changes you made. Settings will stay the same.


##List
Create a job that prints a list with elements.

```json
{"UserId": "asdfasdfasdf",
"Type": "list",
"Items":[
  {"Title":"Title of item 1"},
  {"Title":"Title of item 2"},
  {"Title":"Title of item 3"}
  ...
]
}
```

>Output the same as text

###Query Parameters

Parameter | Default | Possible values | Description	|
--------- | ------- | --------------- |  -----------
Type | list | - | Will print the list.
Items | - | - | The array with the items that must be on the list.





# Change item


```json
{"UserId": "asdfasdfasdf",
"Barcode":"87451247754",
"Action":"add/del/open/delClosed/delOpen"}
```

>The output

```json
{
  "Id": 2,
  "Name": "Monster beer",
  "Barcode": "091991290913213",
  "Closed": 5,
  "Open": 10
}
```



Add or remove an item from the fridge. When sending del to the server, it will first remove the open items and after that it starts with the closed ones.
If the closed or open value equals 0, it won't change a thing, but the same output will be send.


### HTTP Request

`POST /api/changeItem`

### Query Parameters

Parameter | Default | Possible values | Description	|
--------- | ------- | --------------- |  -----------
Barcode | - | - | The barcode of the item
Action | add | add/del/open/delClosed/delOpen | What should be done?


# Change title


```json
{"UserId": "asdfasdfasdf",
"Barcode":"87451247754",
"Title":""}
```

>The output

```json
{
  "Id": 2,
  "Name": "Monster beer",
  "Barcode": "091991290913213",
  "Closed": 5,
  "Open": 10
}
```


Change the name/title of the item.

### HTTP Request

`POST /api/changeTitle`

### Query Parameters

Parameter | Default | Possible values | Description	|
--------- | ------- | --------------- |  -----------
Barcode | - | - | The barcode of the item
Title | - | - | The new title of the item

# Server check



>The output

```json
y
```


This is to check if the url provided is of a smartfridge API.

### HTTP Request

`POST/GET /api/serverCheck`

### Query Parameters

*none*


# User Check


```json
{"UserId": "asdfasdfasdf"}
```

>The output

```json
y/n
```


Used for the app to check if the given userid is correct.

### HTTP Request

`POST /api/userIdCheck`

### Query Parameters

Parameter | Default | Possible values | Description	|
--------- | ------- | --------------- |  -----------
UserId | - | - | The given userId to check
