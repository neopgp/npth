# Makefile.am - src/ Makefile for npth.
# Copyright (C) 2011 g10 Code GmbH
#
# This file is part of NPTH.
#
# NPTH is free software; you can redistribute it and/or modify it
# under the terms of either
#
# - the GNU Lesser General Public License as published by the Free
# Software Foundation; either version 3 of the License, or (at
# your option) any later version.
#
# or
#
# - the GNU General Public License as published by the Free
# Software Foundation; either version 2 of the License, or (at
# your option) any later version.
#
# or both in parallel, as here.
#
# NPTH is distributed in the hope that it will be useful, but WITHOUT
# ANY WARRANTY; without even the implied warranty of MERCHANTABILITY
# or FITNESS FOR A PARTICULAR PURPOSE.  See the GNU Lesser General
# Public License for more details.
#
# You should have received a copy of the GNU Lesser General Public
# License along with this program; if not, see <http://www.gnu.org/licenses/>.

## Process this file with automake to produce Makefile.in

EXTRA_DIST = npth.def
nodist_include_HEADERS = npth.h

lib_LTLIBRARIES = libnpth.la

libnpth_la_SOURCES = npth.h npth.c

# AM_CPPFLAGS =
# AM_CFLAGS =

if HAVE_W32_SYSTEM
RCCOMPILE = $(RC) $(DEFS) $(DEFAULT_INCLUDES) $(INCLUDES)
LTRCCOMPILE = $(LIBTOOL) --mode=compile --tag=RC $(RCCOMPILE)

SUFFIXES = .rc .lo

.rc.lo:
	$(LTRCCOMPILE) -i "$<" -o "$@"

npth_res = versioninfo.lo
no_undefined = -no-undefined
export_symbols = -export-symbols $(srcdir)/npth.def

install-def-file:
	$(INSTALL) $(srcdir)/npth.def $(DESTDIR)$(libdir)/npth.def

uninstall-def-file:
	-rm $(DESTDIR)$(libdir)/npth.def

gpgme_deps = $(gpgme_res) npth.def

else
npth_res =
no_undefined =
export_symbols =
install-def-file:
uninstall-def-file:

npth_deps =
endif

libnpth_la_LDFLAGS = $(no_undefined) $(export_symbols) \
	-version-info \
	@LIBNPTH_LT_CURRENT@:@LIBNPTH_LT_REVISION@:@LIBNPTH_LT_AGE@
libnpth_la_DEPENDENCIES = $(npth_deps)
libnpth_la_LIBADD = @NETLIBS@

install-data-local: install-def-file

uninstall-local: uninstall-def-file
