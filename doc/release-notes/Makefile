DOC	= release

all: html

.PHONY: html ps

html: $(DOC).html
ps: $(DOC).ps

$(DOC).ps: $(DOC).sgml
	linuxdoc -B latex -o ps $(DOC)

#$(DOC).dvi: $(DOC).tex
#	latex $(DOC).tex
#	latex $(DOC).tex
#	latex $(DOC).tex
#


%.txt: %.sgml
	linuxdoc -B txt -T 2 --filter $<

$(DOC).txt: $(DOC).sgml
	linuxdoc -B txt -T 2 --filter $<

%.html: %.sgml
	linuxdoc -B html -T 2 --split=0 $<
	perl -i -p -e "s%$@%%" $@
	perl -i -p -e 's%Bug #(\d+)%Bug <a href="http://www.squid-cache.org/bugs/show_bug.cgi?id=$$1">#$$1</a>%g' $@

$(DOC).html: $(DOC).sgml
	linuxdoc -B html -T 2 --split=0 $(DOC)
	perl -i -p -e "s%$(DOC).html%%" $(DOC).html
	perl -i -p -e 's%Bug #(\d+)%Bug <a href="http://www.squid-cache.org/bugs/show_bug.cgi?id=$$1">#$$1</a>%g' $(DOC).html

%.man: %.sgml
	linuxdoc -B txt -m $<

$(DOC).man: $(DOC).sgml
	linuxdoc -B txt -m $(DOC)

clean:
	rm -f *.html
	rm -f *.tex *.ps *.dvi *.aux *.log *.toc
	rm -f *.txt *.man
