---
author: Thomas
---

# Webrings

- What are webrings?

A collection of websites, linked together in the form of a circle. Together, they form a small "ring" of information / creation.

Example: https://webring.xxiivv.com/

- Why is this relevant?

Webrings are _usually_ controlled by people rather than large companies, of who you know no one.


## Webrings as a DNS


The way I currently envision this, is that people will manage their own DNS through learning about addresses, and saving them as **whatever they like**. This also means that **people can decide whatever domain they'd like to use, and they don't have to pay for it.**

Content providers can give a domain name recommendation, but they can't assume that the domain name will be used by the user.

A domain name recommendation is a name that is recommended by the content owner. Example:

Someone hosts an open source project on `dat://87ed2e3b160f261a032af03921a3bd09227d0a4cde73466c17114816cae43336` - they'd like people to remember this project by its name, so he decides to recommend this `dat` as `beakerbrowser.com`.

Someone learns of this `dat` address, and visits the address. The procedure is as follows:

1. The user's webring will check and see if it knows about this `dat`.
2. If not, the webring will send a request to look for this `dat` locally.
3. If nothing is found, the webring will send a request to look for this `dat` online.
4. If something is found, the webring will check for a [.well-known/dat](https://beakerbrowser.com/docs/guides/use-a-domain-name-with-dat#well-knowndat) file, and use this as a recommended domain name.
