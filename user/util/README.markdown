Tcpcrypt netstat
================

The `util/tcnetstat` program lists active tcpcrypt connections and their
session IDs.

With two HTTP connections open, the output looks like:

    $ test/tcnetstat -N
    Using 1 implementation
    Local address		Foreign address		SID
    128.12.13.14:59539   	171.66.3.211:80      	E0C4FA717D0B3C51E4E2A8EC70CA34ADFC91A260
    128.12.13.14:59540   	171.66.3.211:80      	EA22A7B8A9994AB151A865C5F5AC1309DD674D6C

There is currently a limit of approximately 100 active connections that can be
displayed by tcnetstat. This will be fixed soon and does not affect tcpcryptd.


Tcpcrypt netcat
===============

The `test/tcpcrypt` binary can function like netcat (`nc`). After the
connection is established, the tcpcrypt session ID is printed if the tcpcrypt
negotiation occurred; otherwise, a warning is printed.

To start listening on 127.0.0.1:7777, run:

    test/tcpcrypt -v -l 127.0.0.1 7777

To connect as a client to the server you just started, run:

    test/tcpcrypt -v 127.0.0.1 7777

Port 7777 must have the appropriate firewall rules for tcpcryptd to receive
these packets. The included `launch_tcpcryptd.sh` script will add the correct
rules for port 7777.

Example
-------

Launch the `-l` listen command first, and then launch the connect command in a
separate window. In this example, after the connection was established, "hello!\n"
was typed, followed by Ctrl-C to exit.

    $ test/tcpcrypt -v -l 127.0.0.1 7777
    Listening on 0.0.0.0:7777
    Connection from 127.0.0.1:46170
    Using 1 implementation
    Session ID: F2E4B35E44F39DA32DD57BC9FAA2F5E28C034E54
    hello!
    Connection terminated

    $ test/tcpcrypt -v 127.0.0.1 7777
    Connected from 127.0.0.1:46170 to 127.0.0.1:7777
    Using 1 implementation
    Session ID: F2E4B35E44F39DA32DD57BC9FAA2F5E28C034E54
    hello!
    ^C


Other functions
---------------

The `test/tcpcrypt` binary also can run many other tests and benchmarks (`-h`
for a list).