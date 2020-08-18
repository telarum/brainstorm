---
author: Thomas + zvava
---

# Webrings

- What are webrings?

A collection of websites, linked together in the form of a circle. Together, they form a small "ring" of information / creation. in telarum, webrings are

> an example of a webring on the modern web would be https://webring.xxiivv.com/

- Why is this relevant?

Webrings are _usually_ controlled by people rather than large companies, of who you know no one.

## format of urls in telarum

urls in telarum are simply made up of 5* parts, and each part serves its own important purpose. protocol, port, and data** are optional as the assumed protocol is telarum, the port is assumed to be `70` or `77`, or whatever the protocol's default expected port is, and data can just be blank when requesting the front page of a website. (`/` should be after the name or port anyway)

| protocol[1] | id[2] | name[3] | port[4] | data[5] |
| -: | - | - | :-: | - |
|`telarum://` | `stiffcocks` | `.pizza` | `:70` | `/big/girthy` |

1. the protocol is one of the ones defined as compatible with telarum, or whatever else the user's client supports

2. the id for a specific website, specified in a webring

3. the name for a webring, specified in the webring's configuration

4. the port is as it traditionally is

5. the data can be viewed as a file tree, but it can represent api endpoints etc. depending upon the server.

*there can also be an optional `#anchor` appended to the end of the data to link to a specific point on a page

**attempting to send a request to [what represents] the root of the filesystem should have the client change your request to "main", or the server should serve "main", if your data is "main" then the client should change it to display blank.

## Webrings as a DNS

The way this is currently being envisioned is that people will manage their own "DNS" on their client through learning about addresses or other webrings, and saving them as **whatever they like** - this also means that **people can decide whatever id/name they'd like to use, and they don't have to pay for it**.

Content providers can give a id recommendation, but they can't assume that the id will be used by the user.

An id recommendation is a name that is recommended by the content owner.

### example: `dat` addresses

Someone hosts an open source project on (`dat://`)`87ed2e3b160f261a032af03921a3bd09227d0a4cde73466c17114816cae43336` - they'd like people to remember this project by its name, so he decides to recommend this `dat` as `beakerbrowser`.

Someone learns of this raw `dat` address, and visits the address, their client will recommend them to use a specific id if they don't happen to have one already. The procedure is as follows:

1. The user's client webring will check and see if it knows about the address.

4. If not, the client will send a request to look for this `dat` in the client's webrings list of peers.

3. If not found, the client will send a request to look for this `dat`'s [.well-known/dat](https://beakerbrowser.com/docs/guides/use-a-domain-name-with-dat#well-knowndat) file, and use this as a recommended domain name.

## example webring configuration
- client webring
```toml
# the default name is local
# it can be changed to 'com' or something
name = "local"

[nodes]
fuckyouall = 1.2.3.4
stiffcocks = 2.3.4.5

[peers]
space = 3.4.5.6
```

- hosted webring
```toml
name = "pizza"
info = [
	"this webring is hosted by x",
	"personal homepage/blog: fuckyouall.pizza."
	"it is mainly a collection of video hosting websites",
]

[nodes]
fuckyouall = 1.2.3.4
stiffcocks = 2.3.4.5

[peers]
space = 3.4.5.6
```
