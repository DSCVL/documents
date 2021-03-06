LATEX	= pdflatex -shell-escape
BIBTEX	= bibtex
DVIPS	= dvips
DVIPDF  = dvipdft
XDVI	= xdvi -gamma 4
GH		= gv

EXAMPLES = $(wildcard *.h)
SRC	:= $(shell egrep -l '^[^%]*\\begin\{document\}' *.tex)
TRG	= $(SRC:%.tex=%.dvi)
PSF	= $(SRC:%.tex=%.ps)
PDF	= $(SRC:%.tex=%.pdf)

default: all

pdf: $(PDF)

ps: $(PSF)

$(TRG): %.dvi: %.tex *.bib $(EXAMPLES) *.sty
	$(LATEX) $<
	$(BIBTEX) $(<:%.tex=%)
	$(LATEX) $<
	$(LATEX) $<

$(PSF):%.ps: %.dvi
	$(DVIPS) -R -Poutline -t letter $< -o $@

$(PDF): %.pdf: %.ps
	ps2pdf $< 

show: $(TRG)
	@for i in $(TRG) ; do $(XDVI) $$i & done

showps: $(PSF)
	@for i in $(PSF) ; do $(GH) $$i & done

	
all: pdf
	rm -f *.ps *.dvi *.out *.log *.aux *.bbl *.blg *.pyg *.toc

clean:
	rm -f *.ps *.dvi *.out *.log *.aux *.bbl *.blg *.pyg *.toc

.PHONY: all show clean ps pdf showps