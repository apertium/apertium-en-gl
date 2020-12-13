LANG1=en
LANG2=gl
PREFIX1=$(LANG1)-$(LANG2)
PREFIX2=$(LANG2)-$(LANG1)

BASENAME=apertium-$(PREFIX1)

TARGETS_COMMON = $(PREFIX1).automorf.bin $(PREFIX1).autobil.bin $(PREFIX1).autogen.bin \
                 $(PREFIX1).autopgen.bin $(PREFIX2).automorf.bin $(PREFIX2).autobil.bin \
                 $(PREFIX2).autogen.bin $(PREFIX2).autopgen.bin $(PREFIX1).lextormono.bin $(PREFIX2).lextormono.bin \
                 $(PREFIX1).lextorbil.bin $(PREFIX2).lextorbil.bin \
                 $(PREFIX1).t1x.bin $(PREFIX1).t2x.bin $(PREFIX1).t3x.bin \
                 $(PREFIX2).t1x.bin $(PREFIX2).t2x.bin $(PREFIX2).t3x.bin

TARGETS = $(TARGETS_COMMON)

# This include defines goals for install-modes, .deps/.d and .mode files:
@ap_include@

$(BASENAME).$(LANG1).dix: $(BASENAME).$(LANG1).metadix
	@xsltproc buscaPar.xsl apertium-en-gl.en.metadix | uniq > tmp1gen.xsl
	@xsltproc tmp1gen.xsl apertium-en-gl.en.metadix >$(BASENAME).$(LANG1).dix
	@rm tmp1gen.xsl

$(PREFIX1).automorf.bin: $(BASENAME).$(LANG1).dix
	apertium-validate-dictionary $(BASENAME).$(LANG1).dix
	lt-comp lr $(BASENAME).$(LANG1).dix $@
#	@rm $(BASENAME).$(LANG1).dix

$(PREFIX1).autobil.bin: $(BASENAME).$(PREFIX1).dix
	apertium-validate-dictionary $(BASENAME).$(PREFIX1).dix
##NO TOCAR	apertium-gen-oldbil $(BASENAME).$(PREFIX1).dix tmp$(PREFIX1).autobil.dix
	xsltproc translate-to-default-equivalent.xsl $(BASENAME).$(PREFIX1).dix >tmp$(PREFIX1).autobil.dix
	lt-comp lr tmp$(PREFIX1).autobil.dix $@
	rm tmp$(PREFIX1).autobil.dix

$(PREFIX1).autogen.bin: $(BASENAME).$(LANG2).dix
	apertium-validate-dictionary $(BASENAME).$(LANG2).dix
	lt-comp rl $(BASENAME).$(LANG2).dix $@

$(PREFIX1).autopgen.bin: $(BASENAME).post-$(LANG2).dix
	apertium-validate-dictionary $(BASENAME).post-$(LANG2).dix
	lt-comp lr $(BASENAME).post-$(LANG2).dix $@

$(PREFIX2).automorf.bin: $(BASENAME).$(LANG2).dix
	apertium-validate-dictionary $(BASENAME).$(LANG2).dix
	lt-comp lr $(BASENAME).$(LANG2).dix $@
#	@rm $(BASENAME).$(LANG2).dix

$(PREFIX2).autobil.bin: $(BASENAME).$(PREFIX1).dix
	apertium-validate-dictionary $(BASENAME).$(PREFIX1).dix
##NO TOCAR	apertium-gen-oldbil $(BASENAME).$(PREFIX1).dix tmp$(PREFIX2).autobil.dix
	xsltproc translate-to-default-equivalent.xsl $(BASENAME).$(PREFIX1).dix >tmp$(PREFIX2).autobil.dix
	lt-comp rl tmp$(PREFIX2).autobil.dix $@
	rm tmp$(PREFIX2).autobil.dix

$(PREFIX2).autogen.bin: $(BASENAME).$(LANG1).metadix
	@xsltproc buscaPar.xsl apertium-en-gl.en.metadix | uniq > tmp2gen.xsl
	@xsltproc tmp2gen.xsl apertium-en-gl.en.metadix >$(BASENAME).$(LANG1).dixtmp2
	@rm tmp2gen.xsl
	apertium-validate-dictionary $(BASENAME).$(LANG1).dixtmp2
	lt-comp rl $(BASENAME).$(LANG1).dixtmp2 $@
	@rm $(BASENAME).$(LANG1).dixtmp2
#	@rm $(BASENAME).$(LANG1).metadix
#	@rm $(BASENAME).$(LANG2).dix
#	@rm $(BASENAME).$(LANG1)-$(LANG2).dix

$(PREFIX2).autopgen.bin: $(BASENAME).post-$(LANG1).dix
	apertium-validate-dictionary $(BASENAME).post-$(LANG1).dix
	lt-comp lr $(BASENAME).post-$(LANG1).dix $@

$(PREFIX1).t1x.bin: $(BASENAME).$(PREFIX1).t1x
	apertium-validate-transfer $(BASENAME).$(PREFIX1).t1x
	apertium-preprocess-transfer $(BASENAME).$(PREFIX1).t1x $@

$(PREFIX1).t2x.bin: $(BASENAME).$(PREFIX1).t2x
	apertium-validate-interchunk $(BASENAME).$(PREFIX1).t2x
	apertium-preprocess-transfer $(BASENAME).$(PREFIX1).t2x $@

$(PREFIX1).t3x.bin: $(BASENAME).$(PREFIX1).t3x
	apertium-validate-postchunk $(BASENAME).$(PREFIX1).t3x
	apertium-preprocess-transfer $(BASENAME).$(PREFIX1).t3x $@

$(PREFIX2).t1x.bin: $(BASENAME).$(PREFIX2).t1x
	apertium-validate-transfer $(BASENAME).$(PREFIX2).t1x
	apertium-preprocess-transfer $(BASENAME).$(PREFIX2).t1x $@

$(PREFIX2).t2x.bin: $(BASENAME).$(PREFIX2).t2x
	apertium-validate-interchunk $(BASENAME).$(PREFIX2).t2x
	apertium-preprocess-transfer $(BASENAME).$(PREFIX2).t2x $@

$(PREFIX2).t3x.bin: $(BASENAME).$(PREFIX2).t3x
	apertium-validate-postchunk $(BASENAME).$(PREFIX2).t3x
	apertium-preprocess-transfer $(BASENAME).$(PREFIX2).t3x $@


EXTRA_DIST=$(BASENAME).post-$(LANG1).dix $(BASENAME).post-$(LANG2).dix \
	$(BASENAME).$(LANG1).tsx \
    $(BASENAME).$(LANG2).tsx \
    $(BASENAME).$(LANG1).metadix \
    $(BASENAME).$(LANG2).dix \
    $(BASENAME).$(PREFIX1).dix \
    $(PREFIX1).prob $(PREFIX2).prob \
    buscaPar.xsl principal.xsl \
    translate-to-default-equivalent.xsl \
    $(BASENAME).$(PREFIX1).t1x $(BASENAME).$(PREFIX1).t2x \
    $(BASENAME).$(PREFIX1).t3x $(BASENAME).$(PREFIX2).t1x \
    $(BASENAME).$(PREFIX2).t2x $(BASENAME).$(PREFIX2).t3x \
    modes.xml

apertium_en_gl_DATA=$(PREFIX1).automorf.bin $(PREFIX2).automorf.bin \
    $(PREFIX1).autobil.bin $(PREFIX2).autobil.bin \
    $(PREFIX1).autogen.bin $(PREFIX2).autogen.bin \
    $(PREFIX1).autopgen.bin $(PREFIX2).autopgen.bin \
    $(PREFIX1).prob $(PREFIX2).prob \
    $(PREFIX1).t1x.bin $(PREFIX1).t2x.bin $(PREFIX1).t3x.bin \
    $(PREFIX2).t1x.bin $(PREFIX2).t2x.bin $(PREFIX2).t3x.bin \
    $(BASENAME).$(PREFIX1).t1x $(BASENAME).$(PREFIX1).t2x \
    $(BASENAME).$(PREFIX1).t3x $(BASENAME).$(PREFIX2).t1x \
    $(BASENAME).$(PREFIX2).t2x $(BASENAME).$(PREFIX2).t3x

apertium_en_gldir=$(prefix)/share/apertium/apertium-$(PREFIX1)/
noinst_DATA=modes/$(PREFIX1).mode

install-data-local: install-modes

CLEANFILES = -rf $(TARGETS) modes
