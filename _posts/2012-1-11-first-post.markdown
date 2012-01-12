---
layout: default
title: Installing Python 2.5 in Fedora 12 for Google App Engine
---

*NOTE: This is a test post from my old blog...*

This stupid install process gets me every time! How do you run Google App Engine which currently requires Python2.5 on a machine that has Python2.6 installed? This also goes for anybody trying to use Django with App-Engine.

Everytime I try I get an error like this:

    Traceback (most recent call last):
    File "/home/andriy/lib/google_appengine/dev_appserver.py", line 68, in 
    run_file(__file__, globals())
    File "/home/andriy/lib/google_appengine/dev_appserver.py", line 64, in run_file
    execfile(script_path, globals_)
    File "/home/andriy/lib/google_appengine/google/appengine/tools/dev_appserver_main.py", line 82, in 
    from google.appengine.tools import appcfg
    File "/home/andriy/lib/google_appengine/google/appengine/tools/appcfg.py", line 59, in 
    from google.appengine.tools import appengine_rpc
    File "/home/andriy/lib/google_appengine/google/appengine/tools/appengine_rpc.py", line 32, in 
    https_handler = urllib2.HTTPSHandler
    AttributeError: 'module' object has no attribute 'HTTPSHandler'


Now some people say that you need to "compile python with ssl support". But it ain't so. There is actually nothing to configure in the python install to make it include ssl. Python finds the ssl libraries automatically if they are installed. The trick is you need the dev ssl libraries.


So here it is for my own reference:

    1. Download the openssl-dev packages! Yes... you need them: `sudo yum install openssl-dev*`
    2. Download python2.5
    3. Configure it: `./configure`
    4. Build it: `sudo make`
    5. Alt-install it to make it reside near your current python install: `sudo make altinstall`

Now download App-Engine and make sure to use python2.5 command with it.
