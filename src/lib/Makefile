# Copyright 1993 by Norman Ramsey.  All rights reserved.
# See file COPYRIGHT for more information.

LIB=/dev/null
SHELL=/bin/sh
CINAME=
CIMSG=
RCSFILES=emptydefn toascii.nw autolang.nw unmarkup Makefile nwmtime pipedocs h2a btdefn

all: toascii tominted autolang noweb_lexer.py
	chmod +x unmarkup emptydefn nwmtime pipedocs h2a btdefn

install: all
	cp unmarkup emptydefn toascii tominted autolang noweb_lexer.py nwmtime btdefn $(LIB)
	for i in pipedocs h2a; do \
	  sed "s@|LIBDIR|@$(LIB)@g" $$i > $(LIB)/$$i && chmod +x $(LIB)/$$i; \
	done

uninstall:
	for i in unmarkup emptydefn toascii tominted autolang noweb_lexer.py nwmtime pipedocs h2a btdefn; do \
	  rm -f $(LIB)/$$i; \
	done

source: toascii tominted autolang noweb_lexer.py
touch: toascii tominted autolang noweb_lexer.py
	touch toascii tominted autolang noweb_lexer.py
boot:
	touch toascii tominted autolang noweb_lexer.py

toascii: toascii.nw
	notangle -R$@ toascii.nw > $@
	chmod +x $@

autolang: autolang.nw
	notangle -R$@ autolang.nw > $@
	chmod +x $@

tominted: autolang.nw
	notangle -R$@ autolang.nw > $@
	chmod +x $@

noweb_lexer.py: autolang.nw
	notangle -R'[[noweb_lexer.py]]' autolang.nw > $@

clean:
	rm -f *.log *.blg *.dvi *.toc *.aux *.tex *~
clobber: clean
	rm -f toascii tominted autolang noweb_lexer.py
