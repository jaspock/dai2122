# Minimal makefile for Sphinx documentation

# run before: conda activate dai

# You can set these variables from the command line, and also
# from the environment for the first two.
SPHINXOPTS    ?=
SPHINXBUILD   ?= sphinx-build
SOURCEDIR     = source
BUILDDIR      = build

BROWSER = firefox
SLIDESDIR = source/_static/slides
GITHUBREPO = https://github.com/jaspock/dai2122
GITHUBPAGES = https://jaspock.github.io/dai2122

.PHONY: help Makefile clean push pages slides all open

all: slides html open

# Put it first so that "make" without argument is like "make help".
help:
	@$(SPHINXBUILD) -M help "$(SOURCEDIR)" "$(BUILDDIR)" $(SPHINXOPTS) $(O)

# Catch-all target: route all unknown targets to Sphinx using the new
# "make mode" option.  $(O) is meant as a shortcut for $(SPHINXOPTS).
%: Makefile
	@if [ ! -d $(SLIDESDIR) ]; then \
		echo "directory $(SLIDESDIR) not found!"; \
		echo "run make slides first"; \
		exit 1; \
	fi
	@$(SPHINXBUILD) -M $@ "$(SOURCEDIR)" "$(BUILDDIR)" $(SPHINXOPTS) $(O)

slides:
	@if [ ! -d ../slides/build ]; then \
		echo "directory ../slides/build not found; making slides"; \
		cd ../slides && make; \
	fi;
	rm -rf $(SLIDESDIR); \
	mkdir $(SLIDESDIR); \
	cp -r ../slides/build/* $(SLIDESDIR); \
	echo "slides copied to $(SLIDESDIR)";

open:
	$(BROWSER) build/html/index.html &

pages: slides html
	rm -rf /tmp/gh-pages
	cp -r $(BUILDDIR)/html /tmp/gh-pages
	touch /tmp/gh-pages/.nojekyll
	$(BROWSER) $(GITHUBPAGES) &
	git checkout gh-pages
	cd .. && rm -rf * && cp -r /tmp/gh-pages/* /tmp/gh-pages/.nojekyll . && git add . && \
		git commit -m "Website en gh-pages actualizado" && git push origin gh-pages && \
		git checkout main && git branch
	@echo "move to the parent folder before working on the repository!"

push: clean
	git add -u -v && git commit && git push origin main
	$(BROWSER) $(GITHUBREPO) &

clean:
	rm -rf build $(SLIDESDIR) ../slides/build
