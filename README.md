<img src="http://www.montanamendy.com/bloomberg.png">

Bloomberg Search
=======================

I would usually make this a private repo since it isn't finished, and won't be for awhile since I started updating this again, but I want to keep this open. This is a wrapper around the Java implementation of the Bloomberg API (http://www.bloomberglabs.com/api/about/).

This wrapper acts as a server and is able to receive multiple connections from multiple client implementations.
This is only a prototype of an older version with updated code. This is also referred to in the <a href="https://github.com/bloomberg/chef-bcpc">Chef Bloomberg Recipes</a>.

Being written by <a href="http://www.montanamendy.com">Montana Mendy</a>.

```
JSON Object accepted:
{
    'request':
    {
        'yk_filter': "",
        'query_string': "test",
        'max_results': 10
    }
}
```
yk_filter is optional, leaving it empty means ALL, the other options are YK_FILTER_CRNY, YK_FILTER_EQTY, YK_FILTER_GOVT //TODO add the remaining ones (see Bloomberg API developer guide). 

```
Service secfService = session.getService("//blp/instruments");
Request request = secfService.createRequest("instrumentListRequest");
request.asElement().setElement("query", "IBM");
request.asElement().setElement("yellowKeyFilter", "YK_FILTER_CORP");
request.asElement().setElement("languageOverride", "LANG_OVERRIDE_NONE");
request.asElement().setElement("maxResults", 10);
sendRequest(request, session);
```

Most of this can be accomplished looking at the Bloomberg Labs page, which is right here.

*  http://bloomberg.github.io/blpapi-docs/java/3.9/

The JSON objects should be returned as follows: 

```
JSON Objects returned:
{
    'error': "error msg"
}

{
    'response':
    [
        {
            security: "TEST",
            description: "Description for security TEST"
        },
        ...
    ]
}
```

Objects returned can be an error or a response which contains an array with objects, that contain the security name and description.

Libraries used:

`Bloomberg API Java`: http://www.bloomberglabs.com/api/libraries/ (3.9)
