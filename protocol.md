---
authors: zvava + Thomas
---

# the telarum:// protocol
> every one of these headers are subject to change, once they are all very definitively standardized, ability to use the compressed bytes will be enabled

## terminology

**header**, the same principal as http headers

**e2e**, short for end to end encryption/encrypted

## security/authentication
> e2e is optional *only* for webrings, webrings can also choose if they can be unencrypted or strictly e2e

1. you request a public key from the server
```toml
[auth_request]
# specify if you want your correspondence to be transferred in bytes or in raw toml
# authentication has to be in raw toml
minimize = true | false
# the minimize field is not required, you can just send the auth_request header, it will default to whatever the server can provide/client can receive/default browser option is
```

2. you receive a public key from the server

```toml
[auth_response]
public_key = "{data}"
```

3. you send your public key to the server (encrypted with the server's public key) in the same format as the server sent you theirs

4. now all following requests to/from the server are encrypted

## example telarum request
```toml
data = "main"
# type of file you are expecting to receive
content = "text/page"
# type of compression/encoding you can accept
# the type "none" is default and implied
# if the website can fulfill one of these, it will
encoding = ["gzip","deflate","br", etc.]

[personalize]
# if the website has multiple language support
language = "english"
# alternative to user-agent
# you can specify these if a website provides a different download link for different operating systems, or something
client = "browserName"
os = ""
# supply a username/password to authenticate a request, the telarum request is encrypted already so these can be plain here
username = "thomas"
password = "whatever
```

## example telarum response
> date could be optional

- raw toml
```toml
# status, different from http statuses
status = "OK"
# a mime type
type = "text/page"
# current date yyyy/mm/dd/hh/mm/ss
date = "2020 08 18 14 56 03"
# type of compression/encoding
encoding = "none" | "gzip" | etc.

# then the actual data is sent via tcp or udp packets
```

- compressed bytes
```toml
# each header is started by one byte
# followed by it's arguments in bytes
# and them closed with an 0xff byte

# status, where 01 is OK, 00 would be ERROR, etc.
00 01 ff
# mime type, where 01 is text/page, 00 would be unknown, etc.. there would only be 255 mime types available like this though.
01 01 ff
# date, where there are four bytes dedicated for year, then the remaining cannot exceed 255 so the remaining each can and only take one
02 Y0 Y1 Y2 Y3 MM dd hh mm ss ff
# encoding, where 00 is none, and there are 255 available to encode the data in
03 00 ff

# then the actual data is sent via tcp or udp packets
```
