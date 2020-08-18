---
authors: zvava + Thomas
---

# the telarum:// protocol
> every one of these headers are subject to change, once they are all very definitively standardized, ability to use the compressed bytes will be enabled

the `telarum` protocol is the main protocol used by telarum clients, both for data transfer and resolving urls. telarum is secure by default and utilizes end to end encryption.

- why replace `http`?

`http` is bloated and insecure, and there are too many headers that convey information only important to the "modern" web. telarum aims to provide a slimmer ~~and superior~~ alternative. it is also secure by default - there is no need for a separate protocol that provides encryption over telarum. cookies are also completely removed, and authentication is simplified.

- how is it more secure *and* slimmer?

see the protocol security section; once the keys are exchanged, there is no need to again unless your client forgets the server's key or vice versa. also see the example request/response sections; there aren't only less headers, but they are standardized, allowing for compression down to mere bytes.

## terminology

**header**, the same principal as http headers

**e2e**, short for end to end encryption/encrypted

## protocol security
> e2e is optional *only* for webrings, they can choose if they can be used unencrypted or strictly e2e, there should be *no option* to disable e2e *anywhere **ever***.

end to end encryption [in telarum] works by an exchange of keys. both the client and server have a pair of keys; one private and one public, the public key can encrypt but only the private can decrypt. if the client has the server's public key and vice versa, only the client can decrypt the information given to it by the server and vice versa.

> the client could generate a different key pair for every website, but that might only be for people with some kind of paranoia

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

> if the server forgets the client's public key, changes its private key, or receives a request from the client that it cannot decrypt; it sends a response to the client which indicates an authentication error, which should prompt the client to forget the server's old key and retry authentication

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
