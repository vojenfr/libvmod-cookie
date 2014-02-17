----------------------
Varnish Cookie Module
----------------------

SYNOPSIS
========

import cookie;

DESCRIPTION
===========

project fork -->> https://github.com/lkarsten/libvmod-cookie

FUNCTIONS
=========

new fonctions :

1/ cookie.sort_string();
   The cookies will be classified in alphabetical order.

2/ cookie.count();
   Count cookies numbers.

INSTALLATION
============

The source tree is based on autotools to configure the building, and
does also have the necessary bits in place to do functional unit tests
using the varnishtest tool.

Usage::

 ./configure VARNISHSRC=DIR [VMODDIR=DIR]

`VARNISHSRC` is the directory of the Varnish source tree for which to
compile your vmod. Both the `VARNISHSRC` and `VARNISHSRC/include`
will be added to the include search paths for your module.

Optionally you can also set the vmod install directory by adding
`VMODDIR=DIR` (defaults to the pkg-config discovered directory from your
Varnish installation).

Make targets:

* make - builds the vmod
* make install - installs the vmod in `VMODDIR`
* make check - runs the unit tests in ``src/tests/*.vtc``

In your VCL you could then use this vmod along the following lines::

	import cookie;
	sub vcl_recv {
		cookie.parse(req.http.cookie);
		set req.http.Cookie = cookie.sort_string();
		set req.http.N-Cookie = cookie.count();
	}

