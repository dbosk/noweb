LIB=/dev/null  # to be overridden by install
SHELL=/bin/sh

all: linemark nolinemap
	chmod +x linemark nolinemap

source: linemark nolinemap

linemark: nolinemap.nw
	notangle -Rlinemark nolinemap.nw | cpif linemark
	chmod +x linemark

nolinemap: nolinemap.nw
	notangle -Rnolinemap nolinemap.nw | cpif nolinemap
	chmod +x nolinemap

install: all
	cp linemark nolinemap $(LIB)
	ln -sf nolinemap $(LIB)/noerr

uninstall:
	rm -f $(LIB)/linemark $(LIB)/nolinemap $(LIB)/noerr

touch:
	touch linemark nolinemap

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
