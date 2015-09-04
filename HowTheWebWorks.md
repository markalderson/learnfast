# Learn how the Web works in 10 minutes

Every web developer needs to know a couple of things about how the web works. The details are _really_ complicated,
but the main concepts actually require little effort to be understood.

## Local networks

Local networks are networks of computers somewhat _close_. Perhaps they are in the same house or building.
But actually there aren't real limits, except for technical ones: the transmission medium (e.g. optical fiber, copper, etc.),
the protocol (for example the [CSMA/CD](https://en.wikipedia.org/wiki/CSMA/CD) protocol used in
[Ethernet](https://en.wikipedia.org/wiki/Ethernet) networks requires
limits on the extension of the network, otherwise the communication may be corrupted due to interference between users), etc..

Also, devices like _repeaters_ and _switches_ allow to merge two ore more local networks making a bigger one. So the point is
not how much wide is a local network. The point is that a local network is a network that doesn't address the problem of
connecting all the computers in the world like the Internet does.

There are many types of local network. Some are wired some are wireless. Some follow a protocol, some follow another.

**Note:** a _protocol_ is simply a set of rules that two or more subjects agree to follow when communicating with each other.

Users of a local network communicate by exchanging _packets_ of data. Each user has an _address_ (have you ever heard
about [MAC addresses](https://en.wikipedia.org/wiki/MAC_address)?) and these addresses are used in packets to identify
senders and receivers.

## Internet (TCP / IP)

The Internet is based on the... Internet Protocol (IP). This protocol, also knwon as TCP / IP, was designed in the 70s
at the DARPA (Defence Advanced Research Project Agency). It was designed to connect local networks and it soon
passed from military use to universities. Today is used to connect... the entire world.

**Note:** "Internet" (with capital I) indicates the world-wide network of computers that we know and use
everyday. Instead "internet" (lower case) is used to refer to the protocol or to a generic implementation of it.
Thus, Internet _is a_ internet.

Like on local networks, packets and addresses are used to allow communication. The additional complexity of internet
is in that, given an internet address (the famous _IP address_), it's necessary to know on which local network
resides the corresponding user. If it's on a different local network, the packet will be sent to a _gateway_, a
computer, managed by your ISP (Internet Service Provider), that is responsible
to choose where the packet goes next. Usually it's sent to another computer, managed by the same or another ISP,
until it reaches the correct local network. ISP have to collaborate, in order to allow this process, called
_routing_.

Be aware that:

* there is no guarantee that a packet will make it to its destination (packet loss)
* the order in which packets are sent is not necessarily the same in which they are received: for optimization
reasons, the same receiver may be reached crossing different paths depending on traffic conditions during routing

If the packet does arrive to the receiver's local network, it's necessary to translate the IP address
in a local address. That's easy: since every user of computer in the local network knows both its local and IP addresses,
a message is broadcasted all over the local network, asking "who is the computer with this IP address?".

TCP is a protocol that uses IP to allow a process executed on a computer to communicate with another process (executed
on a computer that may, but doesn't have to, a different one). Processes on a machine are identified by a number called _port_, while IP addresses are re-used by TCP to identify computers.

TCP provides the communication with some qualities that IP doesn't deliver.

Specifically, TCP handles the ordering of received packets and recovers from failures like lost packets and corrupted packets.

**Note:** The corruption of a packet may be detected by inserting some additional data to it. That data is a kind of
signature. If the packet becomes corrupted, the data and the signature won't match.

In short, we say that TCP is _reliable_. TCP is also _connection-oriented_. This means that communication requires opening
and closing a connection. In practice, this means that some resources will be allocated in order allow the protocol
to work correctly.

**Note:** For some kind of services (e.g. multimedia streaming) UDP (User Datagram Protocol) is used instead of TCP
because, not providing reliability, it's faster and doesnt require a connection.

## The Web (HTTP and URI)

In the 90s a couple of protocols were designed at the CERN (European Organization for Nuclear Research) with the goal
of providing a way to exchange hypertexts across the world, forming the so-called World Wide Web (WWW), or simply Web.

The URI (Uniform Resource Identifier, originally Universal Resource Locator, URL) is a protocol defining resource
identifiers. Originally, resource were tipically hyptertexts coded in HTML (HyperText Markup Language), but now
the URI are used to identify a lot of stuff.

Although suitable for use in combination with other protocols, URI was designed to work with HTTP (HyperText Transfer
Protocol).

HTTP is used by a computer called _client_ to request operations on some resources. This requests are issued to a
computer, called _server_, that is able to act on those resources. The communication
is based on TCP connections. The client sends a _request message_, the server responds with a _response message_ and
then the connection is usually closed.

Request and response are both text messages, but they can optionally transfer any kind of file through econding and
decoding.

The first line of a request always indicates the URI of the requested resource and a _method_. HTTP defines several
methods, but GET, POST, PUT, DELETE, HEAD and OPTIONS are the most used. GET and POST, in particular, are the only
ones used by Web Browsers.

The method is an indication about what to do with the resource:

* GET: send back a represantion of state of the resource (e.g. if it's a web page, give me the HTML code)
* POST: create a related resource using the representation included in the request (for example this is sometimes used
by the web browser when a form is submitted in order to create a new post on some web site)
* PUT: create or update the resource using the representation included in the request
* DELETE: delete the resource
* HEAD: send back metadata about that resource
* OPTIONS: send back info about how it's possible to operate on this resource

Note that, apart from GET and POST, these methods are mostly used by the so-called RESTful Web Services (or simply REST APIs),
software systems that use HTTP to exchange data.

As I said, the request indicates the URI of a resource. An HTTP URI follows this syntax:

```
http://<server>:<port>/<path>?<parameters>
```

where:

* `<server>` identifies the server, either by a name (e.g. "google.com") or by an IP address (e.g. "217.22.209.32")
* `<port>` is the TCP port used by the server (the default port is number 80)
* `<path>` is a path like the ones used in local file systems
* `<parameters>` are additional data passed to the server as details about the requested resource

Since public web servers use the default port, it's usually omitted. Also, query parameters are rarely used and,
whe they are, the are mostly used to express search criteria.

This is an example of HTTP URI:

```
http://www.example.com/users/marco/profile
```

HTTP requests and responses both can contain a header and a body. If present, the body contains a resource representation.
The header is used to specify details about the request / response. For example, a common response header is the one used
to specify the content type of the body, in order to allow the client to decode it properly. Some headers are part
of the HTTP standard, but you can also use custom headers for your server, as long as clients know how to interpret them.

Response messages contain a status code that informs about success or failure of the request.

## DNS

The DNS (Domain Name System) is a protocol that handles the conversion from a domain name (e.g. "google.com") to an
IP address. Think of DNS as a huge database split on several computers all over the Internet. When you ask for a page,
your local DNS service asks to one of this computer to translate the name in the URI into an IP address. Usually,
this computer doesn't know the answer, but it does know the address of a computer that knows more than it does.
Eventually, after some delegation steps, you got your answer.

## Cookies

HTTP is a stateless protocol. This means that in order to implement sessions, each request needs to carry some
data to declare itself as part of a specific session. This is tradionally done with _cookies_, small amounts
of data that a server asks its clients to send along with each request.

You can turn cookies off, as they can be used to track your behaviour. But, actually, the server will still
have a lot of ways to implement sessions (or spy on you!).

## HTTPS

It's a safe version of HTTP in which messages are encrypted and the identity of the server may be proved by a
certificate. This is based on [Asymmetric Cryptography](https://en.wikipedia.org/wiki/Public-key_cryptography).
That's complex stuff, though.

## WebSocket

_WebSocket_ is a new protocol designed for web sites that need to push data to the client without waiting for explicit requests. Examples of use are chat systems, real-time news, games. HTTP is used to make the first request, then a
connection is established and both client and server can send each other data without being asked to.

I won't cover the details. For now.

## What to do now

Nothing. Just wait for other tutorials to put these concepts in practice!
