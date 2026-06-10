# Copyright 1993 by Norman Ramsey.  All rights reserved.
# See file COPYRIGHT for more information.

LIB=/dev/null
SHELL=/bin/sh
CINAME=
CIMSG=
RCSFILES=emptydefn toascii.nw tominted.nw unmarkup Makefile nwmtime pipedocs h2a btdefn

all: toascii tominted
	chmod +x unmarkup emptydefn nwmtime pipedocs h2a btdefn

install: all
	cp unmarkup emptydefn toascii tominted nwmtime btdefn $(LIB)
	for i in pipedocs h2a; do \
	  sed "s@|LIBDIR|@$(LIB)@g" $$i > $(LIB)/$$i && chmod +x $(LIB)/$$i; \
	done

uninstall:
	for i in unmarkup emptydefn toascii tominted nwmtime pipedocs h2a btdefn; do \
	  rm -f $(LIB)/$$i; \
	done

source: toascii tominted
touch: toascii tominted
	touch toascii tominted
boot:
	touch toascii tominted

toascii: toascii.nw
	notangle -R$@ toascii.nw > $@
	chmod +x $@

tominted: tominted.nw
	notangle -R$@ tominted.nw > $@
	chmod +x $@

clean:
	rm -f *.log *.blg *.dvi *.toc *.aux *.tex *~
clobber: clean
	rm -f toascii tominted
