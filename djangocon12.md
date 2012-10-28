Day 1: [notes](http://dstegelman-conf-notes.readthedocs.org/en/latest/conferences/djangocon2012/index.html) erickson1019w
Take Two: If I got do it all over again (2-10:15)
----------------------------------------------------
## Problems:
Testing in Django Sucks
  - The universe of inputs is too large
    - settings, db, other global states are too hard to control

- Probably should use jinja2 templates

## Solutions:
No auto generated files
No global state
Everything is a view
Isolated tests

Django and Backbone.js (1-11:05)
-----------------------------------
I should do a talk on this
Hijax


Views can be Classy (2-1:30)
-------------------------------
Good, check out django-braces

Django on Gevent (2-2:20)
-------------------------
## Building concurrent systems
- Processes
  - not scalable
- Threads
  - Non deterministic scheduling
  - nice synchronous interface
- Non-blocking I/O
  - Callbacks (node.js, Reactor Pattern) 
    - One thread manages multiple connections
    - simple things are intuitive, complex things hard
  - coroutines
    - benefits of threads without the non-determinism
    - call stacked preserved

## Greenlet
Provides coroutines in python  

## Gevent
- Expands upon greenbelt to provide green threads
- provides an event loop

## with django
- gunicorn, use worker_class = "gevent"
- psycogreen makes psycopg2 work with gevent
- celery comes with built in support
- gevent-socketio
- ZeroMQ: zmq.green
- HAProxy and Varnish* have websocket support
- gevent.backdoor - get a python shell into your process via telnet
- gevent connection pooling for db's?

5. PostgreSQl when its not your job (1-4:20)
--------------------------------------------
## Setups
- turn off OOM killer
- use ext4 or XFS
- set SHMMAX and SHMALL

## Logging
thebuild.com
- don't use celery/sessions in the db

6. Security Best practices (2-5:10)
-----------------------------------
- django-sha2
- auto-escape annotations
http://coffeeonthekeyboard.com/mozillas-security-best-practices-873/

7. Django ORM
-------------
https://speakerdeck.com/u/malcolmt

Django Forms
------------
django-remote-forms
django-remote-admin

Django Cache
ketama alg
django-pylibmc
Elasticache - was memcache
johnny-cache

nose-progressive
http://lanyrd.com/2012/djangocon-us/coverage/
