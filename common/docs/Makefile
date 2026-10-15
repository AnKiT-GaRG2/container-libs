PREFIX := /usr/local
DATADIR := ${PREFIX}/share
MANDIR := $(DATADIR)/man
GOMD2MAN ?= $(shell command -v go-md2man || echo '$(GOBIN)/go-md2man')
SED ?= sed

docs: $(patsubst %.md,%,$(wildcard *.md))

# Man pages have no link mechanism: turn [text](other-page.md) into plain text.
%.5:  %.5.md
	$(SED) -E -e 's/\[([^]]*)\]\([^):]*\.md(#[^)]*)?\)/\1/g' $^ | $(GOMD2MAN) -out $@

.PHONY: install
install:
	install -d ${DESTDIR}/${MANDIR}/man5
	install -m 0644 *5 ${DESTDIR}/${MANDIR}/man5
	install -m 0644 links/.*.5 ${DESTDIR}/${MANDIR}/man5

.PHONY: clean
clean:
	$(RM) *.5
