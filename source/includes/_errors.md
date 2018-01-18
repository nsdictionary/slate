# Errors

<aside class="notice">
See the error response format on the right side.
</aside>

The Sentbe API uses the following error codes:

Error Code | Meaning
---------- | -------
E0000 | Internal Server Error 
E0001 | Authentication error -- auth_key/ip address
E0002 | Invalid model id
E0003 | Invalid header key
E0004 | Invalid signature
E0005 | Need more required parameter / Unpermitted parameter
E0006 | Not supported method
E0007 | Not available currency
E0008 | Invalid calc_by parameter
E0009 | Invalid transfer status
E0010 | Can't update recipient information
E0011 | Invalid country code
E0012 | Not supported bank

> error response parameter JSON structured like this:

```json
{
  "result": false,
  "errors": [
    {
      "message": "Invalid transfer id",
      "error_code": "E0002"
    }
  ]
}
```
