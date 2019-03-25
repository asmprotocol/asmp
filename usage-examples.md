# Usage Examples

## Check if any version of PHP is available

**URL** : `/check/`

**Method** : `POST`

#### Request

```json
{
	"components": [
		[
			{
				"name": "PHP",
				"constraints": []
			}
		]
	]
}
```

#### Success Responses

**Condition** : Data provided is valid and all requests were understood and supported by the server

**Code** : `200 OK`

**Content example** : Response will include whether all component requests could be fulfilled based on the criteria (in this simple case there is no additional criteria), a component for each requested component group, and the version that would be used to fulfill this request.:

```json
{
	"fulfillable": true,
	"components": [
		{
			"name": "PHP",
			"value": "7.2.9"
		}
	]
}
```

#### Error Response

**Condition** : If provided data is invalid or unsupported.

**Code** : `405 Invalid input`

**Content example** :

```json
{}
```

## Update PHP and MySQL to the best supported version

Change requests are best started with a check request. The returned components array can be fed directly back into the change request exactly as it is returned from the server.

#### Check Request

**URL** : `/check/`

**Method** : `POST`

Check to see if we can get PHP newer than 5.6 and MySQL newer than 5.0 but not 8.0 or higher.

```json
{
	"components": [
		[
			{
				"name": "PHP",
				"constraints": [
					{
						">=": "5.6"
					}
				]
			},
			{
				"name": "MySQL",
				"constraints": [
					{
						">=": "5.0",
						"<": "8.0"
					}
				]
			}
		]
	]
}
```

#### Check Request Successful Response

**Condition** : Data provided is valid and all requests were understood and supported by the server

**Code** : `200 OK`

**Content example** : Response will include whether all component requests could be fulfilled based on the criteria (in this simple case there is no additional criteria), a component for each requested component group, and the version that would be used to fulfill this request.:

```json
{
	"fulfillable": true,
	"components": [
		{
			"name": "PHP",
			"value": "7.3.2"
		},
		{
			"name": "MySQL",
			"value": "5.7.25"
		}
	]
}
```

#### Change Request

**URL** : `/change/`

**Method** : `POST`

For our change request we will pass in a callback URI that will be hit when the actual change happens, and the list of components and their respective values that the server returned from our check request.

```json
{
	"callback": "https://example.com/callback",
	"components": [
		{
			"name": "PHP",
			"value": "7.3.2"
		},
		{
			"name": "MySQL",
			"value": "5.7.25"
		}
	]
}
```

#### Change Request Successful Response

**Condition** : Data provided is valid and all requests were understood and supported by the server

**Code** : `200 OK`

**Content example** : Response will include a message suitable to display and an id that can be used to check the status of the request.:

```json
{
  "message": "string",
  "id": "e38443a5-e6cb-4297-98cc-28eced0d8e7e"
}
```

#### Error Response

**Condition** : If provided data is invalid or unsupported.

**Code** : `405 Invalid input`

**Content example** :

```json
{}
```
