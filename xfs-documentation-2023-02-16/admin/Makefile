#
# design documentation build rules
#
SUBDIRS=XFS_Performance_Tuning

# Never blow away subdirs
.PRECIOUS: $(SUBDIRS)
.PHONY: $(SUBDIRS)

DOCFILES=$(wildcard *.asciidoc)

HTML_TARGETS=$(addsuffix .html, $(basename $(DOCFILES)))
PDF_TARGETS=$(addsuffix .pdf, $(basename $(DOCFILES)))
EPUB_TARGETS=$(addsuffix .epub, $(basename $(DOCFILES)))

%.html: %.asciidoc
	@echo "[html] $*"
	$(Q)a2x -f xhtml $<

%.pdf: %.asciidoc
	@echo "[pdf] $*"
	$(Q)a2x -f pdf $<

%.epub: %.asciidoc
	@echo "[epub] $*"
	$(Q)a2x -f epub $<

default: html pdf epub $(SUBDIRS)

$(SUBDIRS):
	@echo "Building $@"
	$(Q)$(MAKE) $(MAKEOPTS) -q -C $@ || $(MAKE) $(MAKEOPTS) -C $@

html: $(HTML_TARGETS)

pdf: $(PDF_TARGETS)

epub: $(EPUB_TARGETS)

# manually construct build dependencies for target builds so that modification
# of individual files will trigger a rebuild of the document correctly.
$(PDF_TARGETS): $(DOCFILES)

$(HTML_TARGETS): $(DOCFILES)

$(EPUB_TARGETS): $(DOCFILES)

clean: $(addsuffix -clean, $(SUBDIRS))
	$(Q)rm -f *.html *.pdf *.css *.epub

%-clean:
	@echo "Cleaning $*"
	$(Q)$(MAKE) $(MAKEOPTS) -C $* clean
