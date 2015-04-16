# akamai-debug
Set of tools to debug Akamai

The `dns` directory has one directory per country, with dns servers in many cities. The `bin` directory contains the tools.

## Tools

```
bin/georandomdns <dns_file>
```
Receives a filename in the `dns` directory. Returns one random of the IP addresses the file contains.
```
bin/resolvehost <dns> <hostname>
```
Receives the IP address of a DNS server and a hostname to resolve. Returns the IP address that the hostname resolves to, according to the DNS server.
```
bin/ixget <server> <host> [<path>]
```
Receives a server IP address or hostname, a hostname for the `Host` header, and optionally a path, if it's different from `/`. Makes an HTTP request to the server using Akamai's debug directives in the Pragma request header and returns all the response headers.
```
bin/geolookup <ip_address>
```
Receives an IP address. Returns the city, country and continent where it is located, according to Akamai's Edgescape service.
```
bin/httproute <dns_file> <server> <host> [<path>]
```
Makes an HTTP request to the server and parses the debug response headers to show the client-edge-parent-origin route, along with the geolocation of each server involved.

For example, in the following case, a request is made to an Edge server in Iran.
```
guillermo$ bin/httproute dns/ir/tiran old.ir.edgesuite.net old.ir
Using 94.139.183.210 as DNS
94.139.183.210 is located in TEHRAN, IR, AS
Resolving old.ir.edgesuite.net
Using 107.14.43.195 as Edge server
Requesting http://old.ir/ from Edge server
X-Cache: TCP_MISS from a107-14-43-191.deploy.akamaitechnologies.com (AkamaiGHost/7.1.4.1.1-15000561) (-)
107.14.43.191 is located in SECAUCUS, US, NA
X-Cache-Remote: TCP_MISS from a209-170-118-119.deploy.akamaitechnologies.com (AkamaiGHost/7.1.4.1.1-15000546) (-)
209.170.118.119 is located in ASHBURN, US, NA
```
