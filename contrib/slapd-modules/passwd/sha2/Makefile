# $OpenLDAP$

LDAP_SRC = ../../../..
LDAP_BUILD = $(LDAP_SRC)
LDAP_INC = -I$(LDAP_BUILD)/debian/build/include -I$(LDAP_BUILD)/include -I$(LDAP_SRC)/include -I$(LDAP_SRC)/servers/slapd
LDAP_LIB = $(LDAP_BUILD)/debian/build/libraries/libldap_r/libldap_r.la \
	$(LDAP_BUILD)/debian/build/libraries/liblber/liblber.la

LIBTOOL = $(LDAP_BUILD)/debian/build/libtool
CC = gcc
OPT = -g -O2 -Wall
DEFS = 
#DEFS = -DSLAPD_SHA2_DEBUG
INCS = $(LDAP_INC)
LIBS = $(LDAP_LIB)

PROGRAMS = pw-sha2.la
LTVER = 0:0:0

prefix=/usr
exec_prefix=$(prefix)
ldap_subdir=/ldap

libdir=$(exec_prefix)/lib
libexecdir=$(exec_prefix)/libexec
moduledir = $(libdir)$(ldap_subdir)

.SUFFIXES: .c .o .lo

.c.lo:
	$(LIBTOOL) --mode=compile $(CC) $(OPT) $(CFLAGS) $(CPPFLAGS) $(DEFS) $(INCS) -c $<

all:		$(PROGRAMS)

pw-sha2.la:	slapd-sha2.lo sha2.lo
	$(LIBTOOL) --mode=link $(CC) $(OPT) $(LDFLAGS) -version-info $(LTVER) \
	-rpath $(moduledir) -module -o $@ $? $(LIBS)

clean:
	rm -rf *.o *.lo *.la .libs

install:	$(PROGRAMS)
	mkdir -p $(DESTDIR)$(moduledir)
	for p in $(PROGRAMS) ; do \
		$(LIBTOOL) --mode=install cp $$p $(DESTDIR)$(moduledir) ; \
	done

