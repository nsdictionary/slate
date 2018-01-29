# Callback transfer status

## 1. Set callback user
You must register the callback url information to the Sentbe server in advance to receive the transfer status.

<aside class="notice">
e.g. http://example.com/setnbe_callback
</aside>

## 2. Set callback receiver
You need to be able to receive a callback request from your partner's web server so that you can receive the status information from Sentbe. The request information issued from the sentbe server is the same as the right side json format.

### request
Parameter | Description
--------- | -----------
token | partner's access_id
external_id | partner's transfer unique id
status | transfer status

> request parameter JSON structured like this:

```json
{
  "token": "partner_access_id",
  "external_id": "23",
  "status": "Waiting verification"
}
```

<aside class="notice">
For security reasons, you may want to validate <code>token</code> parameter against partner's <code>access_id</code>.
</aside>

<aside class="notice">
The response's http status code <code>200</code>.
</aside>

## 3. Transfer status

- <code>Waiting verification</code>
: Waiting for recipient's verification
- <code>Processing</code>
: Your bank is requesting money transfer
- <code>AML filtered</code>
: AML filter target
- <code>Complete</code>
: Transaction complete
- <code>Canceled</code>
: Transaction canceled
- <code>Expired</code>
: Verification wait timeout
- <code>Refunded</code>
: Refund completed
