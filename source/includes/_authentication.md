# Authentication

## 1. 파트너 인증정보
파트너는 인증 과정에서 등록시 Sentbe가 보낸 세 가지 정보가 필요합니다.

- <code>partner_id</code>
- <code>access_id</code>
- <code>secret_key</code>

<aside class="warning">
<code>access_id</code> 및 <code>secret_key</code>는 비밀 정보입니다. 외부에 노출 시키거나 안전하지 않은 장소에 보관하지 마십시오.
</aside>


## 2. request body 암호화
API를 호출 할 때 전달할 매개 변수가 있다면 json 문자열을 암호화하여 헤더에 넣어야합니다. json 문자열과 함께 미리 발행 된 secret_key를 사용하여 오른쪽의 암호화 로직을 참조하여 매개 변수 정보를 암호화 할 수 있습니다.


> request parameter json string encryption logic

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
  crypt = aes.update(value.to_json) + aes.final()
  encrypted_data = (Base64.strict_encode64(crypt)).strip
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
  data[1..-2].gsub('\\"', '"').gsub('\\n', '')
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
테스트 버전 정보: ruby <code>2.3.1</code>, php <code>7.1.7</code>
</aside>

<aside class="notice">
javascript를 사용하신다면 암호화할때 <code>CryptoJS v3.1.2</code>(https://code.google.com/archive/p/crypto-js/) 라이브러리를 사용해야 합니다.
</aside>

<aside class="notice">
암복호화 로직은 오픈소스인<code> cryptojs-aes-php </code> (https://github.com/brainfoolong/cryptojs-aes-php)를 베이스로 수정해서 사용했습니다.
</aside>


## 3. request header 설정

- <code>Content-Type</code> : "application/json; charset=utf-8"
- <code>PARTNER-ID</code> : 발급받은 파트너 고유 ID
- <code>KEY</code> : 발급받은 파트너 access_id
- <code>SIGNATURE</code> : 전송할 요청 매개 변수가 있으면 <a href="#2-request-body">step 2</a>에서 암호화 된 값

<aside class="notice">
매개 변수를 전송할 필요가없는 엔드 포인트에 대해서는 <code>SIGNATURE</code>를 생략 할 수 있습니다.
</aside>

> request header value structure

```json
{
  "Content-Type" : "application/json; charset=utf-8",
  "PARTNER-ID" : "your partner id here",
  "KEY" : "your access_id here",
  "SIGNATURE" : "encrypted request parameter here"
}
```
