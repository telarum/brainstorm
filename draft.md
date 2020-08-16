---
author: zvava
---

# draft

- what is this draft for?

i made this rough draft to act as a rough outline of the ideas that i had/have now that we are first discussing telarum so we can build off of them in the future. this will make thinking easier as at least some of the idea is written down already and can be reffered back to as to not forget some information.

- why is this so informal and full of (maybes)?

this is a draft. i just want my ideas out of my brain and in a document. the (maybes) will be expanded and fleshed out later once we understand/think more.

- why you talk about using ipv4? isn't it obsolete?

ipv4 is only used here as an example, we could use ipv6, or replace those completely with our own "ipv5" which is just ipv4 but instead of each part being limited up to 255, they can go up 999. (or something)

- what is/are the telarum protocol(s)?

`telarum://` is a protocol with two parts: you can send a request to a server with headers, and you can receive a response with headers and a file. the response is sent in several chunks, the first chunk contains the headers, an index header, and a part of the file - the rest of the chunks only contains indexes and parts of the file.

`telaring://` could be a protocol for interacting with telarum webrings/name servers, ie. to ask for the webring's name, to ask to resolve a domain, 

- what is a telarum url?

a telarum url is made up of 5 parts, the protocol, the id, the name/webring, a port, and some data. the the part that's just the id and the name is refered to as the domain

> eg. protocol://id.name:port/data/

> eg. telarum://stiffcocks.pizza:70/big/girthy/dicks
>
> where telarum:// = protocol (potentially obsolete, we are making a new standard after all), stiffcocks = id, pizza = name, :70 = port, /big/girthy/dicks/ = essentially the same as whatever http has, except there are no get headers (login.html/?user=asdf) but instead you only have the headers in the protocol ie. no GET, only POST, but better because there is only one type of request

## example
1. you run a telarum server on a computer (eg. a raspi) which is connected to a router, the router authenticates the server and it receives an ip, now with 192.168.0.69:70 (70 can be the default port ig) on the local network you can access the site hosted on the telarum server.

2. you run a telarum webring on another computer (perhaps somehow the same computer(maybe different ports? (maybe current dns servers use different ports idk lol))) which is connected to the same router, it gets assigned another ip 192.168.0.42 which uses :77 for dns (or smth), the dns.yaml/ini/etc names the dns server "pizza", and points "stiffcocks" to [insert one of the two following scenarios]

### in the case of an external network
3. a. "localhost" (which automatically evaluates to the webring's external ip by clients).

4. a. now you are able to port forward the webring and the server on the router, and now the router's external ip which has been decided to be 1.2.3.4 (*somehow* uniquely) can be used as a webring and also gives the website hosted on 1.2.3.4 a domain, improving the ux of that website (need idea on how to host multiple websites on one network and have multiple exposed).

5. a. you could also specify a listing option in dns.yaml/ini/etc, which would (*somehow*) cause it to find other networks, and join a webring channel, the default webring chanel could just be "public" (which is given as the value of the listing option). as a member of that webring, you can discover other webrings by querying your webring.

### in the case of a local network
3. b. "192.168.0.69" (which is the ip of our website).

4. b. now other clients on the local network are able to use 192.168.0.42 as a local webring server to connect to multiple local websites, and maybe some other external websites.

5. b. you would discover other webrings via. word of mouth or some sort of central instance of one (think of mastodon and the other activitypub federated social networks, or matrix (which plans to disable open registration when it is mature enough and other instances are available))

### the client
6. you also run a telarum client on another computer (whatever device you have access to, the telarum client could be from within browser, or a daemon that manage's the whole device's internet connectivity then browsers contact the daemon to access the internet or however it currently works currently idk lmao) which has a list of dns servers that it uses, of which one is [1.2.3.4 or 192.168.0.42], and on the client boot the name of that item is requested.

7. when "stiffcocks.pizza" is typed into the url bar. the client then asks pizza (1.2.3.4 or 192.168.0.42) if it has an entry for stiffcocks, it does and it redirects to [localhost or 192.168.0.69], so we send a request to that ip with our /data/ and headers. it returns a file and it is the browser's job to render the response - whether as a website or a dialog to save a file (picture, binary, video, audio).
