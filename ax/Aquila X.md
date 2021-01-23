# Aquila X

## UI

- All Aquila X UI implementation should follow a standard input and output irrespective of the design variations.

  Aquila X text search interface resembles any other search engine, which consist of an input field along with a search button. Search results are rendered in the UI by parsing `_render` key in search results returned as JSON as defined below.

- text JSON template
```json
      {
      "template": "text",
      "data": {
      		"text": "<some text>"
      	}
      }
```

- media card JSON template

```json
    {
    "template":"card",
    "data": {
    		"title": "<some title>",
    		"description": "<some description>",
    		"image": "<image url>",
    		"video": "<video url>",
    		"audio": "<audio url>",
    		"link": "<url>"
    	}
    }
```

- product card JSON template

```json
    {
    "template":"product",
    "data": {
    		"title": "<some title>",
    		"description": "<some description>",
    		"image": "<image url>",
    		"video": "<video url>",
    		"audio": "<audio url>",
    		"link": "<url>",
    		"price": "<price>",
    		"offer": "<% offer applied>",
    		"coupon": "<coupon code>",
    		"source": {
    			"title": "<coupon code>",
    			"url": "<url>"
    	}
    }
```

- page JSON template

```json
    {
    "template": "page",
    "data": {
    		"title": "<page title>",
        	"thumbnail": "<url to image>",
        	"link": "<url to page>",
        	"description": "<some description>"
    	}
    }
```

- suggestion JSON template

```json
    {
    "template": "suggest",
    "data": {
    		"text": "<suggestion>"
    	}
    }
```

- quick reply JSON template

```json
    {
    "template": "quickreply",
    "data": [{
    		"title": "<some title>",
    		"payload": [{
    			"text": "<payload text>",
    			"code": "<code vector>"
    		}]
    	}]
    }
```

- KG node JSON template

```json
    coming soon
```



## X API

[GET] / get status of Aquila X

request:

```json
{}
```

response:

```json
{
    "success": <Boolean>,
    "message": <String>
}
```



[POST] /login 

request:

```
coming soon
```

response:

```
coming soon
```



[POST] /index 

request:

```json
{
	"html": "<html string>",
	"url": "<website url>"
}
```

response:

```json
{
    "success": <Boolean>,
    "message": <String>
}
```



# Aquila X functionalities

### Index

Aquila X node should allow end users to index text data (received from /index API) into Aquila DB. A default database should be created and used if not specified by the end user.

### Search

Aquila X node should perform search operation on Aquila DB on behalf of end user to fetch data to be displayed.

### Render

Aquila X should follow `_render` template JSON to properly display search results to the end user.