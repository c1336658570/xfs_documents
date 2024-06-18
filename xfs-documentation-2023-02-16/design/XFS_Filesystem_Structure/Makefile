#
# design documentation build rules
#
TARGET=xfs_filesystem_structure

DOCFILES=$(wildcard *.asciidoc) \
	 docinfo.xml

HTML_TARGET=$(addsuffix .html, $(TARGET))
PDF_TARGET=$(addsuffix .pdf, $(TARGET))
EPUB_TARGET=$(addsuffix .epub, $(TARGET))

default: html pdf epub

%.html: %.asciidoc
	@echo "[html] $*"
	$(Q)a2x -f xhtml -d book $<

%.pdf: %.asciidoc
	@echo "[pdf] $*"
	$(Q)a2x -f pdf -d book $<

%.epub: %.asciidoc
	@echo "[epub] $*"
	$(Q)a2x -f epub -d book $<

html: $(HTML_TARGET)

pdf: $(PDF_TARGET)

epub: $(EPUB_TARGET)

# manually construct build dependencies for target builds so that modification
# of individual files will trigger a rebuild of the document correctly.
$(PDF_TARGET): $(DOCFILES)

$(HTML_TARGET): $(DOCFILES)

$(EPUB_TARGET): $(DOCFILES)

clean:
	$(Q)rm -f *.html *.pdf *.css *.epub

