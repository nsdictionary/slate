## 2. Encryption authorization key
Make <code>partner_id</code> and <code>access_id</code> a string such as <code>"partner_id:access_id"</code> and encryption sha256 using secret_key.

> authentication key generation code

```ruby
require 'openssl'
require 'base64'

partner_id = '1'
access_id = 'test_id'
secret_key = 'test_pw'

data = "#{partner_id}:#{access_id}"
digest  = OpenSSL::Digest.new('sha256')
auth_key = Base64.encode64(OpenSSL::HMAC.digest(digest, secret_key, data)).strip
p auth_key 
```

```php
<?php
$partner_id = '1';
$access_id = 'test_id';
$secret_key = 'test_pw';

$data = $partner_id . ':' . $access_id;
$auth_key = base64_encode(hash_hmac('sha256', $data, $secret_key, true));
echo $auth_key;
```

```javascript
<script src="https://cdnjs.cloudflare.com/ajax/libs/crypto-js/3.1.2/rollups/hmac-sha256.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/crypto-js/3.1.2/components/enc-base64-min.js"></script>

<script>
	var partner_id = '1',
    access_id = 'test_id',
    secret_key = 'test_pw';

	var data = partner_id + ':' + access_id;
	var hash = CryptoJS.HmacSHA256(data, secret_key);
	var auth_key = CryptoJS.enc.Base64.stringify(hash);

	console.log(auth_key);
</script>
```

<aside class="notice">
The <code>partner_id</code>, <code>access_id</code>, and <code>secret_key</code> must use pre-assigned values.
</aside>

<aside class="notice">
If you use javascript, use the <code>CryptoJS v3.1.2</code>(https://code.google.com/archive/p/crypto-js/) library.
</aside>
