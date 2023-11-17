include mathfiles

density=-r90x90

.SUFFIXES:
.SUFFIXES: .tex .gif .katex .html

# translate ps file to ppm, crop to minimum background, and translate ppm
# to gif with white (background) transparent
#
.tex.gif:
	TEXINPUTS=.:../..:$(TEXINPUTS);\
	echo | latex $* &&\
          dvips -f < $*.dvi |\
          gs -q -dNOPAUSE -dSAFER -sDEVICE=ppmraw -sOutputFile=-\
          ${density} - |\
          pnmcrop |\
          ppmtogif -transparent white > $*.gif
	/bin/rm -f $*.dvi $*.log $*.aux
	test -f $*.gif && chmod 644 $*.gif

.katex.html:
	$(KATEX) -i $*.katex -o $*.html --macro-file katexmacros --trust
	test -f $*.html && chmod 644 $*.html

ifeq ($(KATEX),)
all: ${gifs}
else
all: ${htmls}
endif

${gifs}: mathmacros

${htmls}: katexmacros

clean: ; /bin/rm -f *.gif *.html Make.out
