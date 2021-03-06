# Captive Landing System #

When a request comes in for a site and you're not logged in to the captive portal, part of the captivity process is redirecting that request back to the captive portal page.  This also needs to be done in a way that has some funny HTTP headers (so that the client doesn't try to ever cache it) and that can handle requests from any site.

There is a Debian init script with defaults file which will allow this to run as a daemon.

There is one implementation of this handler here:

## TPROXY-based handler ##

The TPROXY-based handler is in `tproxy.py`.  This is the new setup.  It uses the IP_TRANSPARENT options and listens for stuff sent by the TPROXY target in iptables.  It runs it's own web server that doesn't have to bind to an address, and acts like a transparent proxy server.  Only it answers all requests with a redirect.

Once the user is logged on and has quota, neither of these scripts handle web requests.

This requires Linux 2.6.28 or later.

## CGI-based handler ##

This handler has been removed because it is no longer supported in the tollgate backend.
