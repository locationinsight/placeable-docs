# Placeable Workbench API v2

This is an updated version of the Placeable Workbench read/write REST API. In addition to the core query, add, edit, & remove functionality this API has new endpoints that give insights into change history.


## Authorization

The API is secured using a pre-shared appKey & appId. Each request to the API must have these parameters, or the service will respond with an HTTP status code of 400.

<b>Example:</b>

	https://workbench.placeable.com/v2/collection?appId=12345678&appKey=abcdefghijklmnopqrstuvwxyz000000
	
NOTE: The appKey & appId have been omitted from all other examples in the documentation for brevity and clarity.


## General Information

<b>Changing Multiple items</b>

For all POST, PATCH, & DELETE calls multiple updates are made by sending multiple calls. 

<b>HTTP vs. HTTPS</b>

Any of the calls outlined in this document can be made as HTTP or HTTPS.

<b>X-UserEmail Header</b>

This header is required for all calls and allows the application to track what user makes what changes. The value for this header should be an email address that easily identifies the requester as the api.

<b>Definitions</b>
<ul>
<li>Collection: A single data set that belongs to a specific brand.</li>
<li>Item: A single entity within a collection.</li>
</ul>


## View Specific Collection

<b>Method:</b> GET

<b>Required Header:</b> 
<ul>
<li>X-UserEmail - [emailAddress]</li>
</ul>

<b>URL:</b>

	/v2/collection/[collectionId]

<b>Example:</b>

	/v2/collection/543309812f1111620d0e21ba
	
<b>Response:</b>

```json
  {
    "id": "543309812f1111620d0e21ba",
    "name": "US Post Office",
    "planId": "56d5db251579e00900bcee2d",
    "fieldMapping": {
      "Store Code": "id",
      "Name": "text",
      "Address Line 1": "street",
      "City": "city",
      "State": "state",
      "Postal Code": "postal",
      "Country Code": "country",
      "Main Phone": "phone",
      "Fax": "phone",
      "Home Page": "url",
      "Hours": "hours",
      "Latitude": "latitude",
      "Longitude": "longitude",
      "Categories": "text",
      "Images": "image",
      "Description": "text"
    },
    "serviceMapping": {
      "3rd_Party_Compare": "56d8db881600000f00c14o51",
      "fileId": "56d2db000b0000d412cjad01"
    },
    "searchFields": [
      "Store Code",
      "Name",
      "Address Line 1",
      "City",
      "State",
      "Postal Code",
      "Country Code",
      "Main Phone"
    ],
    "duplicateFields": [],
    "active": true,
    "dateCreated": 1456855802010,
    "lastUpdated": 1456855845544
  }
```


## View Multiple Items

<b>Method:</b> GET

<b>Required Header:</b> 
<ul>
<li>X-UserEmail - [emailAddress]</li>
</ul>

<b>URL:</b>

	/v2/collection/[collectionId]/items

<b>Example:</b>

	/v2/collection/543309812f1111620d0e21ba/items
	
<b>Response:</b>

```json
{
  "results": [
    {
      "id": "543309812f1111620d0e21ba",
      "refId": "56cf4b3d0e00001f00a6376f",
      "fields": {
          "Store Code": "123",
          "Name": "Placeable",
          "Address Line 1": "2601 Blake St",
          "City": "Denver",
          "State": "CO",
          "Postal Code": "80205",
          "Country Code": "US",
          "Main Phone": "(855) 433-7133",
          "Fax": "",
          "Home Page": "www.placeable.com",
          "Hours": "2:08:00:18:00,3:08:00:18:00,4:08:00:18:00,5:08:00:18:00,6:08:00:18:00",
          "Latitude": "39.7602575",
          "Longitude": "-104.9893168",
          "Categories": "111111",
          "Images": "https://www.placeable.com/uploadsLogo.png",
          "Description": "Be found by your customers."
      },
      "errors": [
        {
          "error": "TextValidation:upper",
          "field": "Store Name",
          "msg": "Field 'Store Name' is not all uppercase."
        }
      ],
      "suggestions": [],
      "conflicts": [],
      "created": "2016-02-25T18:43:11+0000",
      "verified": false,
      "metaData": {
      },
      "loc": [
        "39.7602575",
        "-104.9893168"
      ]
    },
    {
      "id": "543309812f1111620d0e21ba",
      "refId": "56cf4b3d0e00001f00a6376f",
      "fields": {
          "Store Code": "456",
          "Name": "ACME INC",
          "Address Line 1": "2010 Parker Ave",
          "City": "Wheat Ridge",
          "State": "CO",
          "Postal Code": "80033",
          "Country Code": "US",
          "Main Phone": "(855) 555-7654",
          "Fax": "",
          "Home Page": "www.acme.com",
          "Hours": "2:09:00:17:30,3:09:00:17:30,4:09:00:17:30,5:09:00:17:30,6:09:00:17:30",
          "Latitude": "40.4652575",
          "Longitude": "-105.1013168",
          "Categories": "222222",
          "Images": "https://www.acme.com/logo.png",
          "Description": ""
      },
      "errors": [],
      "suggestions": [],
      "conflicts": [],
      "created": "2016-02-25T18:43:11+0000",
      "verified": false,
      "metaData": {
      },
      "loc": [
        "40.4652575",
        "-105.1013168"
      ]
    }
  ],
  "count": 2
}
``` 


## View Specific item

<b>Method:</b> GET

<b>Required Header:</b> 
<ul>
<li>X-UserEmail - [emailAddress]</li>
</ul>

<b>URL:</b>

	/v2/collection/[collectionId]/item/[itemId]

<b>Example:</b>

	/v2/collection/543309812f1111620d0e21ba/item/123
	
<b>Response:</b>

```json
  {
    "id": "543309812f1111620d0e21ba",
    "refId": "56cf4b3f0e00001f00a6376f",
    "fields": {
        "Store Code": "123",
        "Name": "Placeable",
        "Address Line 1": "2601 Blake St",
        "City": "Denver",
        "State": "CO",
        "Postal Code": "80205",
        "Country Code": "US",
        "Main Phone": "(855) 433-7133",
        "Fax": "",
        "Home Page": "www.placeable.com",
        "Hours": "2:08:00:18:00,3:08:00:18:00,4:08:00:18:00,5:08:00:18:00,6:08:00:18:00",
        "Latitude": "39.7602575",
        "Longitude": "-104.9893168",
        "Categories": "111111",
        "Images": "https://www.placeable.com/uploadsLogo.png",
        "Description": "Be found by your customers."
    },
    "errors": [
      {
        "error": "TextValidation:upper",
        "field": "Store Name",
        "msg": "Field 'Store Name' is not all uppercase."
      }
    ],
    "suggestions": [],
    "conflicts": [],
    "created": "2016-02-25T18:43:11+0000",
    "verified": false,
    "metaData": {
    },
    "loc": [
      "39.7602575",
      "-104.9893168"
    ]
  }
  ```


## Basic Search

Search for items based on values within any of the fields outlined in the "searchFields" section of the collection. The search will look for exact matches to the query string. A search for "Colorado" would return items in the state of "Colorado" and also items with an address of "123 Colorado Blvd".

<b>Method:</b> GET

<b>Required Header:</b> 
<ul>
<li>X-UserEmail - [emailAddress]</li>
</ul>

<b>Required Parameters:</b>
<ul>
<li>q: The value that you would like to search for.</li>
</ul>
<b>Optional Parameters:</b>
<ul>
<li>limit: The maximum number of items returned by the search (not more than 25 items will be returned ever).</li>
<li>offset: The number of items that should be skipped.</li>
</ul>
<b>URL:</b>

	/v2/collection/[collectionId]/items?q=[value]&limit=[1-25]&offset=[n]

<b>Example:</b>

	/v2/collection/543309812f1111620d0e21ba/items?q="CO"&limit=25&offset=0

<b>Response:</b>

One or more items matching the query. 

If no items match the query you will recieve the following response:

```json
{
  "results": [],
  "count": 0
}
```


## Advanced Search

Search for items based on field specific values. All user fields should be prefixed with the value of "fields." in the payload of the request.

<b>Method:</b> POST

<b>Required Headers:</b> 
<ul>
<li>X-UserEmail - [emailAddress]</li>
<li>Content-Type - application/json</li>
</ul>

<b>URL:</b>
  
    /v2/collection/[collectionId]/search

<b>Body:</b>

```json
{
    "q" : [
        {
        "operator":"[contains | equals | not_contains]", 
        "field":"[fields.fieldName]", 
        "value":"[fieldValue]", 
        "filter":"[and | or]"
        }
    ],
    "offset": 0,
    "limit" : 25
}
```

<b>Example:</b>

    /v2/collection/543309812f1111620d0e21ba/search

<b>Body:</b>

```json
{
    "q" : [
        {
        "operator":"contains", 
        "field":"fields.State", 
        "value":"CO", 
        "filter":"and"
        }
    ],
    "offset": 0,
    "limit" : 25
}
```

<b>Response:</b>

One or more items matching the query. 

If no items match the query you will recieve the following response:

```json
{
  "results": [],
  "count": 0
}
```


## Adding a New item

<b>Method:</b> POST

<b>Required Headers:</b> 
<ul>
<li>X-UserEmail - [emailAddress]</li>
<li>Content-Type - application/json</li>
</ul>

<b>URL:</b>

	/v2/collection/[collectionId]/item
	
<b>Body:</b>

```json
	{
    "[idField]": "[newItemId]",
    "[optionalField]": "[fieldValue]"
  }
```

<b>Notes:</b>
<ul>
<li>The only field that is required to create a new item is the field identified on the collection as "id".  The value sent for that field must not be a duplicate of any other item in the colletion and must not be blank.</ul>
</ul>

<b>Example:</b>

	/v2/collection/543309812f1111620d0e21ba/item
	
<b>Example Body:</b>

```json
	{
    "Store Code": "111",
    "Name": "New Item",
    "Address Line 1": "123 Main St",
    "City": "Denver",
    "State": "CO",
    "Postal Code": "80033",
    "Country Code": "US",
    "Main Phone": "(111) 111-1111",
  }
```

<b>Response:</b>

The newly created item formatted to match the field list of all other items in the collection.


## Updating an Existing item

<b>Method:</b> PATCH

<b>Required Headers:</b> 
<ul>
<li>X-UserEmail - [emailAddress]</li>
<li>Content-Type - application/json</li>
</ul>

<b>URL:</b>

	/v2/collection/[collectionId]/item/[itemId]

<b>Body:</b>

```json
	[
		{ 
			"op" : "update",
			"field": "[fieldName]", 
			"value" : "[fieldValue]"
		}
	]
```

<b>Example:</b>

	/v2/collection/543309812f1111620d0e21ba/item/123

<b>Example Body:</b>

```json
	[
		{ 
			"op" : "update",
			"field": "Main Phone", 
			"value" : "(222) 222-2222"
		},
		{ 
			"op" : "update",
			"field": "City", 
			"value" : "Boulder"
		}
	]
```

<b>Response:</b>

The patched item with the updated value(s).


## Deleting an Existing item

<b>Method:</b> DELETE

<b>URL:</b>

	/v2/collection/[collectionId]/item/[itemId]
	
<b>Example:</b>

	/v2/collection/543309812f1111620d0e21ba/item/123
	
<b>Response:</b>

"true"


## Pulling A List of Custom Export Templates & Recipes

<b>Method:</b> GET

<b>Required Headers:</b> 
<ul>
<li>X-UserEmail - [emailAddress]</li>
</ul>

<b>Optional Parameters:</b>
<ul>
<li>recipeType: The type of recipe that you would like to query. To find all custom file templates set the type to "custom"</li>
</ul>

<b>URL:</b>

	/v2/collection/[collectionId]/recipes?recipeType=custom
	
<b>Example:</b>

	/v2/collection/543309812f1111620d0e21ba/recipes?recipeType=custom
	
<b>Response:</b>

```json
[  
  {
    "id": "5717234c0b00004900d72g44",
    "collectionId": "543309812f1111620d0e21ba",
    "name": "New Custom File",
    "transformations": [],
    "recipeType": "custom",
    "templateId": "521f9d4b170000n3e8d8bb2t",
    "queryFilter": []
  }
]
```


## Creating a File

<b>Method:</b> GET

<b>Required Headers:</b> 
<ul>
<li>X-UserEmail - [emailAddress]</li>
</ul>

<b>Optional Parameters:</b>
<ul>
<li>type: The format of the file you would like to export. Available options are "csv" & "tsv". If no type is specified the file will export as a "xlsx".</li>
<li>recipeId: The Id of a recipe that should be applied to the export. A recipe may transform or filter data.</li>
</ul>

<b>URL:</b>

	/v2/collection/[collectionId]/export/[templateId]
	
<b>Example:</b>

	/v2/collection/543309812f1111620d0e21ba/export/521f9d4b170000n3e8d8bb2t
	
<b>Response:</b>

```json
{
	"fileId":"571ga59117000090add4cb30"
}
```


## Checking Export Status

<b>Method:</b> GET

<b>Required Headers:</b> 
<ul>
<li>X-UserEmail - [emailAddress]</li>
</ul>

<b>URL:</b>

	/v2/collection/[collectionId]/export/status[fileId]
	
<b>Example:</b>

	/v2/collection/543309812f1111620d0e21ba/export/status/571ga59117000090add4cb30
	
<b>Response:</b>
<ul>
<li>404 Status Code: The file Id has not yet been saved in the database</li>
<li>202 Status Code: The file is being processed</li>
<li>200 Status Code: The file is ready to download</li>
</ul>


## Downloading a File

<b>Method:</b> GET

<b>Required Headers:</b> 
<ul>
<li>X-UserEmail - [emailAddress]</li>
</ul>

<b>URL:</b>

	/v2/collection/[collectionId]/file/[fileId]
	
<b>Example:</b>

	/v2/collection/543309812f1111620d0e21ba/file/571ga59117000090add4cb30
	
<b>Response:</b>

The fields and values included in the template & recipe.
