# $Id$
# Public domain.

include ../Common.mak

test:
# needs plain
	$(env) $(prog) fracden.tex

test2:
	$(pdftex2) -ini f1.tex
	$(pdftex2) -ini f2.tex

prev24:
	$(pdftex2) -ini -jobname=fd-pdftex24 -interaction=nonstopmode fracden.tex
#	pdftype fd-pdftex24.pdf fd-pdftex24.typ

prev25:
	$(pdftex2) -ini -jobname=fd-pdftex25 -interaction=nonstopmode fracden.tex
#	pdftype fd-pdftex25.pdf fd-pdftex25.typ

prev:
	$(MAKE) pdftex2="tl24 pdftex" prev24
	$(MAKE) pdftex2="tl25 pdftex" prev25
	diff --text fd-pdf*.typ

clean:
	$(clean)
