
## WHAT IS IT?

sods is a socket over dns server that uses the DNS to tunnel data. sods
includes a small, portable client (sdt) and ds, a utility to scan for
DNS servers that support recursion.

The protocol is interoperable with OzymanDNS
(<http://lmgtfy.com/?q=OzymanDNS>).


## WHAT DO I NEED TO BUILD IT?

Not much.

sods has been built on Ubuntu Linux, Maemo, OpenWRT, Mac OS X and
Solaris.


## HOW DO I BUILD IT?

### Server

    cd sods
    ./configure
    # adjust the Makefile
    make

### Client

    cd sdt
    ./configure
    # adjust the Makefile
    make


## HOW DO I RUN IT?

    # In the sods directory
    sudo ./sods -vvvv -d /tmp -L 127.0.0.1:22 a.example.com # if you have an SSH server on localhost
    
    # In the sdt directory
    ssh -o ProxyCommand="./sdt -r 127.0.0.1 sshdns.a.example.com" 127.0.0.100
    
    # As a TCP proxy
    ./sdt p 23233 -r 127.0.0.1 sshdns.a.example.com
    ssh -p 23233 localhost # for OpenSSH

The sods client works best with GNU screen installed on your shell
server (see the scripts directory for an example of a script to
reconnect if the connection is dropped).


## WHY WOULD I WANT TO USE IT?

sods is tiny, easily ported and fast. Well, sort of fast, for a
tunnel going over DNS. Which means not really very fast.

sods has a few tricks to get around network limitations.

Some ways to use sods:

* use of gated internet access that allow DNS queries, like those found
in airports, coffee shops, restaurants and hotels, when you just need
quick SSH access

* to bypass firewall port or proxy filtering and snooping

* penetration testing: bypass strict access controls on outgoing
connections on secure networks

* have fun with anyone doing traffic analysis on your network usage


## FEATURES

* use TXT, CNAME or NULL records to encapsulate data

* supports multiple forwarded sessions (use multiple "-L" option)

* round robin packets between name servers

* bounce connections off of public recursive name servers (-r random)

* dynamic backoff/throttling of client

* client can use be used as a pipe (for OpenSSH) or as a TCP proxy (for other ssh clients)


## TODO

* remove hardcoded options and use define, e.g., nobody/nogroup

* multiplex connections to the TCP proxy
