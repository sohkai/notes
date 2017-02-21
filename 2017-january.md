January 2016
============

Tech
----

### LLVM for Grad Students

[Article](https://www.cs.cornell.edu/~asampson/blog/llvm.html)

- LLVM is much more useful than just for hacking on compilers and other research!
- LLVM's IR (intermediate representation) is awesome because it's actually human readable (similar to RISC machine code) unlike most other compilers

### Why Haskell

[Article](http://blog.ezyang.com/2010/01/why-haskell/)

### Socket Programming HOWTO

[Article](https://docs.python.org/3/howto/sockets.html)

- Just use `INET` (i.e. IPv4) and `STREAM` (i.e. TCP) sockets

### Under the Hood: Building and open-sourcing RocksDB

[Article](https://www.facebook.com/notes/facebook-engineering/under-the-hood-building-and-open-sourcing-rocksdb/10151822347683920)

- Embeddable database: skips network overhead (potentially makes queries twice as slow)
- Traditional databases don't have good locking strategies to scale well with multiple cores (making them unable to max out available storage IOPS)

### The History of RocksDB

[Article](http://rocksdb.blogspot.de/2013/11/the-history-of-rocksdb.html)

- The advent of flash memory meant that network latency became a much higher cost to performance than before (0.5% impact with disk vs. 50% impact with flash)

### You Might Not Need a WebSocket

[Article](http://blog.fanout.io/2014/06/24/you-might-not-need-a-websocket/)

- Web realtime users usually want to data sync, not actually have bidirectional streams
- Why not build a nicer abstraction for end use case (e.g. pub/sub, data sync) rather than falling back to a stream?

### To AMQP or to XMPP, that is the question

[Article](https://www.opensourcery.co.za/2009/04/19/to-amqp-or-to-xmpp-that-is-the-question/)

- Don't use XMPP if all you want is a message queue

### Disable Your Antivirus Software (Except Microsoft's)

[Article](http://robert.ocallahan.org/2017/01/disable-your-antivirus-software-except.html)

- Antivirus software generally sucks, they can kill your product


Life
----


Random
------

### P vs NP survey article

[Article](http://www.scottaaronson.com/blog/?p=3095)

- "On the Internet, it is do or do not. There is no disclaim."
