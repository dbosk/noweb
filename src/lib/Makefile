# Copyright 1993 by Norman Ramsey.  All rights reserved.
# See file COPYRIGHT for more information.

LIB=/dev/null
SHELL=/bin/sh
CINAME=
CIMSG=
RCSFILES=emptydefn toascii.nw tominted.nw unmarkup Makefile nwmtime pipedocs h2a btdefn

all: toascii tominted noweb_lexer.py
	chmod +x unmarkup emptydefn toascii tominted nwmtime pipedocs h2a btdefn

install: all
	cp unmarkup emptydefn nwmtime btdefn tominted noweb_lexer.py $(LIB)
	sed 's@|LIBDIR|@$(LIB)@g' pipedocs > $(LIB)/pipedocs
	sed 's@|LIBDIR|@$(LIB)@g' toascii > $(LIB)/toascii
	sed 's@|LIBDIR|@$(LIB)@g' h2a > $(LIB)/h2a
	chmod +x $(LIB)/pipedocs $(LIB)/toascii $(LIB)/h2a

uninstall:
	for i in unmarkup emptydefn toascii tominted noweb_lexer.py nwmtime h2a btdefn; do rm -f $(LIB)/$$i; done
	rm -f $(LIB)/pipedocs

source: toascii tominted noweb_lexer.py
touch: toascii tominted noweb_lexer.py
	touch toascii tominted noweb_lexer.py
boot:
	touch toascii tominted noweb_lexer.py

toascii: toascii.nw
	notangle -R$@ toascii.nw > $@
	chmod +x $@

tominted: tominted.nw
	notangle -R$@ tominted.nw > $@
	chmod +x $@

noweb_lexer.py: tominted.nw
	notangle -R'[[noweb_lexer.py]]' tominted.nw > $@

clean:
	rm -f *.log *.blg *.dvi *.toc *.aux *.tex *~
clobber: clean
	rm -f toascii tominted noweb_lexer.py
