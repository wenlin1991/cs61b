# Documentation Makefile.
# Targets:
#	default: Produces gjdb.dvi using latex2e
#	pdf: Produces gjdb.pdf, using dvips and ps2pdf.
#	clean: Removes reproducible files

SRCDIR = /Volumes/Study/2015winter/cs61b/lab_p/lab7/gjdb-6.4.1/doc

DOCDIR = /Users/linwen/share/gjdb/doc

LATEX = latex

DVIPS = dvips -f

PS2PDF = ps2pdf

.PHONY: default pdf install clean

default: gjdb.dvi 

pdf: gjdb.pdf

gjdb.pdf: gjdb.ps
	$(PS2PDF) gjdb.ps

gjdb.ps: gjdb.dvi
	$(DVIPS) gjdb.dvi > gjdb.ps

gjdb.dvi: $(SRCDIR)/gjdb.tex.in $(SRCDIR)/../Makefile.in $(SRCDIR)/Makefile.in
	version="`sed -n -e 's/^VERSION *= *//p' $(SRCDIR)/../Makefile.in`"; \
	rm -f gjdb.tex
	sed "s/[?][?][?][?]/$$version/" $(SRCDIR)/gjdb.tex.in > gjdb.tex
	TEXINPUTS=$(SRCDIR):$(TEXINPUTS) $(LATEX) gjdb.tex < /dev/null
	TEXINPUTS=$(SRCDIR):$(TEXINPUTS) $(LATEX) gjdb.tex < /dev/null

clean:
	rm -f *~ *.aux *.log *.out 
	rm -f *.dvi *.ps *.pdf

install: pdf
	-mkdir -p $(DOCDIR)
	-cp gjdb.pdf $(DOCDIR)

Makefile: $(SRCDIR)/Makefile.in
	@if [ -r ../config.status ]; then \
	  cd ..; \
	  CONFIG_FILE=doc/Makefile; export CONFIG_FILE; . config.status; \
	fi
