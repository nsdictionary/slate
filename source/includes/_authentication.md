# Authentication

## 1. Get partner access information
You need three pieces of information sent from Sentbe in advance in the certification process.

- <code>partner_id</code>
- <code>access_id</code>
- <code>secret_key</code>

<aside class="warning">
The <code>access_id</code> and <code>secret_key</code> are secret information. Do not expose it outside or store it in a location that is not secure.
</aside>


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


## 3. Encryption request body
If you have parameters to pass when calling api, you should encrypt the json string and put it in the header.
You can encrypt the parameter information by referring to the encryption logic on the right using the secret_key that has been issued in advance with the json string.

> request parameter json string 암복호화 로직

```ruby
require 'openssl'
require 'base64'
require 'json'

def encrypt(key, value)
  salt = Random.new.bytes(8) # generate random bytes

  salted = '';
  dx = '';
  while salted.length < 48
    dx = Digest::MD5.digest("#{dx}#{key}#{salt}")
    salted = "#{salted}#{dx}"
  end

  key = salted[0..31] # key must be 32 in length
  iv = salted[32..-1] # iv must be 16 in length

  # AES encryption
  aes = OpenSSL::Cipher::Cipher.new('AES-256-CBC')
  aes.encrypt
  aes.key = key
  aes.iv = iv
  crypt = aes.update(value) + aes.final()
  encrypted_data = (Base64.encode64(crypt)).strip
  data = {"ct" => encrypted_data, "iv" => bin2hex(iv), "s" => bin2hex(salt)}

  data.to_json
end

def decrypt(key, jsonString, nonce=nil)
  key =  interleave(key, nonce) unless nonce.nil?
  jsondata = JSON.parse(jsonString)

  begin
    salt = hex2bin(jsondata["s"])
    iv  = hex2bin(jsondata["iv"])
  rescue
    return nil
  end

  ct = Base64.decode64(jsondata["ct"])
  concatedPassphrase = "#{key}#{salt}"
  md5 = [];
  md5[0] = Digest::MD5.digest(concatedPassphrase)
  result = md5[0]
  for i in 1..2
    md5[i] = Digest::MD5.digest("#{md5[i-1]}#{concatedPassphrase}")
    result = "#{result}#{md5[i]}"
  end
  key = result[0..32]

  # AES decryption
  decode_cipher = OpenSSL::Cipher::Cipher.new('AES-256-CBC')
  decode_cipher.decrypt
  decode_cipher.key = key
  decode_cipher.iv = iv
  data = decode_cipher.update(ct)
  data << decode_cipher.final()
  data
end

def bin2hex(s)
  s.unpack('H*').first
end

def hex2bin(s)
  s.scan(/../).map { |x| x.hex }.pack('c*')
end

secret_key = 'test_pw'
request_parameter = '{
	"bank_attributes": {
		"name": "002",
		"account_number": "12341234",
		"account_holder_name": "json"
	},
	"country": "KR",
	"phone_country_code": "KR",
	"birth_date": "19901111",
	"external_id": "1",
	"email": "test@sentbe.com",
	"user_id": "47",
	"phone_number": "010-3369-1481",
	"test": "aaa",
	"last_name": "Smith",
	"first_name": "John"
}'

# encryption test
enc = encrypt(secret_key, request_parameter);
puts enc

# decryption test
dec = decrypt(secret_key, enc);
puts dec
```

```php
<?php
function encrypt($key, $value){
    $salt = openssl_random_pseudo_bytes(8);

    $salted = '';
    $dx = '';
    while (strlen($salted) < 48) {
        $dx = md5($dx.$key.$salt, true);
        $salted .= $dx;
    }
    $key = substr($salted, 0, 32); // key must be 32 in length
    $iv  = substr($salted, 32,16); // iv must be 16 in length

    # AES encryption
    $encrypted_data = openssl_encrypt(json_encode($value), 'aes-256-cbc', $key, true, $iv);
    $data = array("ct" => base64_encode($encrypted_data), "iv" => bin2hex($iv), "s" => bin2hex($salt));

    return json_encode($data);
}

function decrypt($key, $value){
    $jsondata = json_decode($value, true);
    try {
        $salt = hex2bin($jsondata["s"]);
        $iv  = hex2bin($jsondata["iv"]);
    } catch(Exception $e) {
		return null;
	}

    $ct = base64_decode($jsondata["ct"]);
    $concatedPassphrase = $key.$salt;
    $md5 = array();
    $md5[0] = md5($concatedPassphrase, true);
    $result = $md5[0];
    for ($i = 1; $i < 3; $i++) {
        $md5[$i] = md5($md5[$i - 1].$concatedPassphrase, true);
        $result .= $md5[$i];
    }

    # AES decryption
    $key = substr($result, 0, 32);
    $data = openssl_decrypt($ct, 'aes-256-cbc', $key, true, $iv);

    return json_decode($data, true);
}

$secret_key = 'test_pw';
$request_parameter = '{
	"bank_attributes": {
		"name": "002",
		"account_number": "12341234",
		"account_holder_name": "json"
	},
	"country": "KR",
	"phone_country_code": "KR",
	"birth_date": "19901111",
	"external_id": "1",
	"email": "test@sentbe.com",
	"user_id": "47",
	"phone_number": "010-3369-1481",
	"test": "aaa",
	"last_name": "Smith",
	"first_name": "John"
}';

# encryption test
$enc = encrypt($secret_key, $request_parameter);
var_dump($enc);

# decryption test
$dec = decrypt($secret_key, $enc);
var_dump($dec);
```

```javascript
<script src="https://cdnjs.cloudflare.com/ajax/libs/crypto-js/3.1.2/rollups/aes.js"></script>
<script type="text/javascript">
var CryptoJSAesJson = {
    stringify: function (cipherParams) {
        var j = {ct: cipherParams.ciphertext.toString(CryptoJS.enc.Base64)};
        if (cipherParams.iv) j.iv = cipherParams.iv.toString();
        if (cipherParams.salt) j.s = cipherParams.salt.toString();
        return JSON.stringify(j);
    },
    parse: function (jsonStr) {
        var j = JSON.parse(jsonStr);
        var cipherParams = CryptoJS.lib.CipherParams.create({ciphertext: CryptoJS.enc.Base64.parse(j.ct)});
        if (j.iv) cipherParams.iv = CryptoJS.enc.Hex.parse(j.iv);
        if (j.s) cipherParams.salt = CryptoJS.enc.Hex.parse(j.s);
        return cipherParams;
    }
}

function encrypt(key, value){
	return CryptoJS.AES.encrypt(JSON.stringify(value), key, {format: CryptoJSAesJson}).toString();
}

function decrypt(key, value){
	return JSON.parse(CryptoJS.AES.decrypt(value, key, {format: CryptoJSAesJson}).toString(CryptoJS.enc.Utf8));
}

var secret_key = "test_pw";
var	request_parameter = `
{
	"bank_attributes": {
		"name": "002",
		"account_number": "12341234",
		"account_holder_name": "json"
	},
	"country": "KR",
	"phone_country_code": "KR",
	"birth_date": "19901111",
	"external_id": "1",
	"email": "test@sentbe.com",
	"user_id": "47",
	"phone_number": "010-3369-1481",
	"test": "aaa",
	"last_name": "Smith",
	"first_name": "John"
}
`;

// encryption test
var enc = encrypt(secret_key, request_parameter);
console.log(enc);

// decryption test
var dec = decrypt(secret_key, enc);
console.log(dec);
</script>

```

<aside class="notice">
Test version information: ruby <code>2.3.1</code>, php <code>7.1.7</code>
</aside>

<aside class="notice">
The encryption decryption logic is based on the open source <code> cryptojs-aes-php </code> (https://github.com/brainfoolong/cryptojs-aes-php).
</aside>


## 4. Set request header

- <code>Content-Type</code> : "application/json; charset=utf-8"
- <code>PARTNER-ID</code> : The partner ID
- <code>KEY</code> : Authentication key encrypted in <a href="#2-encryption-authorization-key">step 2</a>
- <code>SIGNATURE</code> : If there is a request parameter to be transmitted, the value encrypted in <a href="#3-encryption-request-body">step 3</a>

<aside class="notice">
You can omit <code>SIGNATURE</code> for endpoints that do not need to send parameters.
</aside>

> request header value structure

```json
{
  "Content-Type" : "application/json; charset=utf-8",
  "PARTNER-ID" : "your partner id here",
  "KEY" : "encrypted authorization key here",
  "SIGNATURE" : "encrypted request parameter here"
}
```
