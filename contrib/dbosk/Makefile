LIB=/dev/null  # to be overridden by install
MAN=           # optional: man root (e.g. /usr/local/man); empty = skip
MANDIR=$(MAN)/man1
SHELL=/bin/sh

all: linemark nolinemap linemark.1 nolinemap.1
	chmod +x linemark nolinemap

source: linemark nolinemap linemark.1 nolinemap.1

linemark: nolinemap.nw
	notangle -Rlinemark nolinemap.nw | cpif linemark
	chmod +x linemark

nolinemap: nolinemap.nw
	notangle -Rnolinemap nolinemap.nw | cpif nolinemap
	chmod +x nolinemap

linemark.1: nolinemap.nw
	notangle -Rlinemark.1 nolinemap.nw | cpif linemark.1

nolinemap.1: nolinemap.nw
	notangle -Rnolinemap.1 nolinemap.nw | cpif nolinemap.1

install: all
	cp linemark nolinemap $(LIB)
	ln -sf nolinemap $(LIB)/noerr
	if [ -n "$(MAN)" ]; then \
	  mkdir -p $(MANDIR); \
	  cp linemark.1 nolinemap.1 $(MANDIR); \
	  chmod 644 $(MANDIR)/linemark.1 $(MANDIR)/nolinemap.1; \
	  ln -sf nolinemap.1 $(MANDIR)/noerr.1; \
	fi

uninstall:
	rm -f $(LIB)/linemark $(LIB)/nolinemap $(LIB)/noerr
	if [ -n "$(MAN)" ]; then \
	  rm -f $(MANDIR)/linemark.1 $(MANDIR)/nolinemap.1 $(MANDIR)/noerr.1; \
	fi

touch:
	touch linemark nolinemap linemark.1 nolinemap.1

test: all
	notangle -Rexample.py -filter ./linemark example.nw > example.py
	@if command -v python3 >/dev/null 2>&1; then \
	  ./nolinemap python3 example.py > test.out 2>&1; \
	  grep 'example\.nw", line 13' test.out >/dev/null && \
	  grep 'example\.nw", line 8'  test.out >/dev/null && \
	  echo "test passed" || \
	  { echo "test FAILED:"; cat test.out; exit 1; }; \
	else \
	  echo "python3 not found; skipping nolinemap run test"; \
	fi

nolinemap.tex: nolinemap.nw
	noweave -index nolinemap.nw > nolinemap.tex

clean:
	rm -f *.tex *.log *.aux *.dvi *.pdf *.toc *~ example.py test.out

clobber: clean
