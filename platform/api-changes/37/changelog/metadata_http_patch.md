# Breaking change in HTTP PATCH payload

The old HTTP PATCH where you could send in a subset of a payload to patch an object is now gone and instead replaced with JSON Patch ([RFC 6902](https://tools.ietf.org/html/rfc6902)).

As an example, if you want to change the name of a object, before you would do

```json
{
    "name": "New Name"
}
```

Now you will need to follow the format of a JSON Patch and use the format

```json
[
    {"op": "add", "path": "/name", "value": "New Name"}
]
```

You can read more about JSON Patch at [jsonpatch.com](http://jsonpatch.com/).
