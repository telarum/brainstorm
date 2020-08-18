---
author: Thomas + zvava
---

# Webrings

- What are webrings?

A collection of websites, linked together in the form of a circle. Together, they form a small "ring" of information / creation.

> an example of a webring on the modern web would be https://webring.xxiivv.com/

- Why is this relevant?

Webrings are _usually_ controlled by people rather than large companies, of who you know no one. webrings in telarum act as a replacement to traditional dns servers.

- terminology

here is some basic terminology to help you understand the rest of the document: in their configuration files webrings have one word names, like `pizza`, and multiple one word "dns records"/ids for multiple ips/nodes. they can also contains ids for other webrings/peers.

that little tl;dr should provide some more context for the further parts of this document.

- won't it be slow always querying multiple dns servers?

maybe, that's why in the api section there is a possibility to request the webring's whole configuration (or hash of it, for updates), allowing the client to sync with the dns and perform multiple [slightly/somewhat?] faster filesystem operations. (or optionally the client can allow storing this information in ram when it starts for much faster name resolving)

## format of urls in telarum

urls in telarum are simply made up of 5* parts, and each part serves its own important purpose. protocol, port, and data** are optional as the assumed protocol is telarum, the port is assumed to be `70` or whatever the protocol's default expected port is, and data can just be blank when requesting the front page of a website. (`/` should be after the name or port anyway)

| protocol[1] | id[2] | name[3] | port[4] | data[5] |
| -: | - | - | :-: | - |
|`telarum://` | `stiffcocks` | `.pizza` | `:70` | `/big/girthy` |

1. the protocol is one of the ones defined as compatible with telarum, or whatever else the user's client supports

2. the id for a specific website, specified by a webring in its list of nodes (ie. dns records)

3. the name of a webring, specified by a webring in its metadata (the metadata includes the name, and other info describing the webring itself)

4. the port is as it traditionally is

5. the data can be viewed as a file tree, but it can represent api endpoints etc. depending upon the server.

*there can also be an optional `#anchor` appended to the end of the data to link to a specific point on a page

**attempting to send a request to [what represents] the root of the filesystem should have the client change your request to "main", or the server should serve "main", if your data is "main" then the client should change it to display blank.

## Webrings as a DNS

The way this is currently being envisioned is that people will manage their own "DNS"/webring on their client. when learning about addresses or other webrings, users can save them as **whatever they like** - this also means that **people can decide whatever id/name they'd like to use, and they don't have to pay for it**. they can also host their webring for other users to discover.

Website owners can give a recommendation for what id their site should have, but they can't assume that the id will be used by the user.

### example: recommended ids

> this should also apply to `telarum` servers and not just `dat`s, the examples were just written this way initially

Someone hosts an open source project on (`dat://`)`87ed2e3b160f261a032af03921a3bd09227d0a4cde73466c17114816cae43336` - they'd like people to remember this project by its name, so he decides to recommend `beakerbrowser` as its id.

Someone visits this this raw `dat` address, their client will redirect them to use a specific id and name if they have a webring that knows of it, or recommend them to add a specific id to their [local] webring. The procedure is as follows:

1. The user's client webring will check and see if it knows about the address.

2. If not, the client will send a request to look for this `dat` in the client's webrings list of peers.

3. If not found, the client will send a request to look for this `dat`'s [.well-known/dat](https://beakerbrowser.com/docs/guides/use-a-domain-name-with-dat#well-knowndat) file, and use this as a recommended domain name.

### example: resolving webring urls

> this should also apply to `telarum` servers and not just `dat`s, the examples were just written this way initially

the same person who discovered this `dat` would also like people to remember this project by its name, so he decides to call this dat `beakerbrowser` in their webring called `pizza`.

Someone who uses the webring types `beakerbrowser.pizza` into their url bar or clicked on the link on the webring's homepage. the procedure is as follows:

1. The user's client webring will check and see if it knows about the address.

2. The client will also send a request to look for this `dat` in the client's webrings list of peers.

3. if multiple matches are found, the client should ask the user which webring they would like to handle the request from*. if no matches are found, the client should display an error page.

*this shouldn't happen, as clients could give users the option to assign aliases to webrings that happen to have the same name as others (see next section)

## webring configurations

webrings are configured with `toml`. there are two types of webrings; local and external. the client has its own webring that is not publicly available to other users, these are called local webrings and are mainly used to store your favorite webrings and sometimes websites. webrings which are publicly hosted are called external, and are available for use by clients to store many websites, all with a specific topic/theme or just a soup.

- example local webring configuration
```toml
# the default name for client webrings is local
# it can be changed to 'com' or something
name = "local"
# ips of hosted webrings
webrings = [
	"3.4.5.6",
]

# "dns records"
[nodes]
fuckyouall = "1.2.3.4"
stiffcocks = "2.3.4.5"

# aliases for conflicting webrings
[webrings]
space = "3.4.5.6"
```

- example external webring configuration
```toml
# the name for the hosted webring
# will be used as the name in a url by clients
name = "pizza"
# information about the webring to be either requested by clients or displayed on the webring's homepage ("text records")
info = [
	"this webring is hosted by x",
	"personal homepage/blog: fuckyouall.pizza"
	"this webring exists mainly to provide a collection of video hosting websites",
]

# "dns records"
[nodes]
fuckyouall = "1.2.3.4"
stiffcocks = "2.3.4.5"

# ips of other hosted webrings
[peers]
space = "3.4.5.6"
```

## api

[this section addresses communicating with dns servers through the telarum protocol]
