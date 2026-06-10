WWW=$(HOME)/www/noweb/examples
SHELL=/bin/sh
NOTANGLE=nountangle -m3
NOWEAVE=noweave

.SUFFIXES: .i3 .m3 .nw .tex .dvi .html
.nw.html:
	$(NOWEAVE) -filter l2h -filter btdefn -index -html $< > $@
.nw.tex:
	$(NOWEAVE) -index -filter btdefn $< > $@
.nw.i3:
	$(NOTANGLE) -Rinterface -L'<* LINE %L "%F" *>%N' $< > $@
.nw.m3:
	$(NOTANGLE) -L'<* LINE %L "%F" *>%N' $< > $@
.tex.dvi:
	latex '\scrollmode \input '"$*"; while grep -s 'Rerun to get cross-references right' $*.log; do latex '\scrollmode \input '"$*"; done

HTML=breakmodel.html compress.html dag.html graphs.html mipscoder.html primes.html \
	scanner.html test.html tree.html wc.html wcni.html


www: $(HTML)
	copy -v $(HTML) $(WWW)
	copy -v README.h $(WWW)/index.html

clean:
	rm -f *~ *.aux *.tex *.dvi *.log *.html *.toc *.pdf *.idx *.ilg *.ind *.out
	rm -rf _minted fib

clobber: clean

compress.html: compress.nw
	$(NOWEAVE) -filter l2h -index -autodefs c -html compress.nw > $@
compress.tex: compress.nw
	$(NOWEAVE) -index -autodefs c compress.nw > $@
dag.html: dag.nw
	$(NOWEAVE) -filter l2h -index -autodefs icon -html dag.nw > $@
dag.tex: dag.nw
	$(NOWEAVE) -index -autodefs icon dag.nw > $@
# fib.tex is highlighted with minted; fib-xref.tex is the classic
# rendering, in which identifier uses inside code are hyperlinked.
# Both need pdflatex -shell-escape (minted runs Pygments); see
# README.python.
fib.tex: fib.nw
	$(NOWEAVE) -delay -autodefs python3 -index -filter tominted fib.nw > $@
fib-xref.tex: fib.nw
	$(NOWEAVE) -delay -autodefs python3 -index fib.nw > $@
fib.pdf: fib.tex
	mkdir -p _minted
	pdflatex -shell-escape fib.tex
	pdflatex -shell-escape fib.tex
fib-xref.pdf: fib-xref.tex
	pdflatex -shell-escape fib-xref.tex
	pdflatex -shell-escape fib-xref.tex
# The tangled Makefile would clobber this one, so fib tangles into
# its own subdirectory; -t8 keeps the tabs make needs.
fib/fib.py: fib.nw
	mkdir -p fib
	notangle -R'[[fib.py]]' fib.nw > $@
fib/Makefile: fib.nw
	mkdir -p fib
	notangle -t8 -R'[[Makefile]]' fib.nw > $@
fib-run: fib/fib.py fib/Makefile
	$(MAKE) -C fib test
	$(MAKE) -C fib run
mipscoder.html: mipscoder.nw
	$(NOWEAVE) -filter l2h -index -autodefs sml -html mipscoder.nw > $@
mipscoder.tex: mipscoder.nw
	$(NOWEAVE) -autodefs sml -index mipscoder.nw > $@
scanner.html: scanner.nw
	$(NOWEAVE) -filter l2h -index -autodefs c -autodefs yacc -html scanner.nw > $@
scanner.tex: scanner.nw
	$(NOWEAVE) -index -autodefs c -autodefs yacc scanner.nw > $@
tree.html: tree.nw
	$(NOWEAVE) -filter l2h -index -autodefs icon -html tree.nw > $@
tree.tex: tree.nw
	$(NOWEAVE) -index -autodefs icon tree.nw > $@
test.html: test.nw
	$(NOWEAVE) -filter l2h -html test.nw > $@
test.tex: test.nw
	$(NOWEAVE) test.nw > $@
wc.html: wc.nw2html
	$(NOWEAVE) -autodefs c -filter btdefn -index -html -n wc.nw2html > $@
wcni.html: wc.nw2html
	$(NOWEAVE) -filter btdefn -x     -html -n wc.nw2html > $@
wc.tex: wc.nw
	$(NOWEAVE) -autodefs c -filter btdefn -index wc.nw > $@
