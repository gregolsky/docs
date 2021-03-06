﻿# What host should I use? IIS or Windows Service?

## IIS: Best to be used when the RavenDB is publicly accessible on the interwebs

- Pros: 
    - you get the benefits of the IIS management tools, monitoring and tracking abilities,
    - designed for small-to-large requests/hits,
    - heaps of security tests and much better support by security products (DDOS protection, IDS systems etc.),
    - it is battle hardened and experienced.

- Cons:
    - you might need to add the IIS specific configuration (such as increasing maximum request time for bulk inserts), for certain scenarios
    - lots of config options means you might mess something up,
    - recycle times (unless settings changed),
    - generally, a bit of work is required to setup.

## Windows Service: Fine if in a private network.

- Pros:
    - easy to setup - just part of the normal install process,
    - available if IIS installation is not an option.
- Cons: 
    - not tested for large requests or battle hardened for security.

There are no real performance considerations between running in the IIS mode or running in the Service mode. 
Both options are supported and the choice is mostly about what is easier for your ops team to support.


## Where to put RavenDB data?

- RavenDB data should be in the fastest drive on the machine (especially indexes).
- You should put it in the root drive, specifically because that make it more visible and avoid issues such as admin deleting the IIS folder thinking there is nothing in there.
- Take a look at [data settings](../configuration/configuration-options#data-settings) section of configuration options article to properly configure paths.

## Resource usage in test / staging / production environments

Depending on your needs and available infrastructure you may use a different approaches to setup deployment environments. 
You have to consider all possible pros and cons, especially with regards to resource usage. Note that CPU, memory and I/O resources are shared between
RavenDB instances running on the same machine. Such configuration is prone to cause problems because the resources consumed by one instance can impact work of another one.
For example an error in the test could cause high resource consumption that would impact a production database.
Of course everything is very specific to your database throughput, power of machine etc. and might be not a problem for you. 
However to avoid such scenario, the best would be to have all environments on separate servers. The perfect test / staging machine would be identical
to production. Having identical sets of CPUs, memory and storage in both environments means that you can run performance testing with confidence.

