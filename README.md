# Protocol-Buffers-Web-Tokens
Protocol Buffers based web token (JSON Web Token Alternative)

- Smaller token size
- Faster decoding
- Standardized encryption standard

## Creation process

```
base64_url_encode(header) + "." +
base64_url_encode(body) + "." +
base64_url_encode(signature or nonce)
```

## Structure of the Signature

### Signing only

----

#### HMAC-SHA-256

----

```
body = payload
signature = HMAC_SHA256(
	base64_url_encode(header) +
	"." +
	base64_url_encode(body),
	signingKey
)
```

#### HMAC-SHA-384

----

```
body = payload
signature = HMAC_SHA384(
	base64_url_encode(header) +
	"." +
	base64_url_encode(body),
	signingKey
)
```

#### HMAC-SHA-512

----

```
body = payload
signature = HMAC_SHA512(
	base64_url_encode(header) +
	"." +
	base64_url_encode(body),
	signingKey
)
```

### Authenticated encryption

----

#### AEAD-AES128-GCM

----

```
nonce = (12 bytes of random)
header = nonce
//Key length is 16 bytes (128 bits)
body = AES-GCM(nonce, key, payload)
```

#### AEAD-AES256-GCM

----

```
nonce = (12 bytes of random)
header = nonce
//Key length is 32 bytes (256 bits)
body = AES-GCM(nonce, key, payload)
```

#### AEAD-CHACHA20-POLY1305

----

[RFC8439](https://www.rfc-editor.org/rfc/rfc8439.html)

```
nonce = (12 bytes of random)
header = nonce
body = ChaCha20_Poly1305(nonce, key, payload)
```

