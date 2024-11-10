# Minimal makefile for Sphinx documentation
#

PYTHON := $(shell command -v python3 || command -v python)
MAKE_VENV := $(PYTHON) -m venv
VENV := ./venv-$(shell uname -s)

# You can set these variables from the command line, and also
# from the environment for the first two.
SPHINXOPTS    ?=
SPHINXBUILD   ?= $(VENV)/bin/sphinx-build
SOURCEDIR     = .
BUILDDIR      = _build

# Put it first so that "make" without argument is like "make help".
.PHONY: help
help: $(SPHINXBUILD)
	@$(SPHINXBUILD) -M help "$(SOURCEDIR)" "$(BUILDDIR)" $(SPHINXOPTS) $(O)

.PHONY: clean
clean:
	rm -rf _build
	rm -rf $(VENV)

.PHONY: venv
venv: $(VENV)

$(VENV): requirements.txt
	$(PYTHON) -c 'import sys; sys.exit(0 if sys.version_info >= (3, 8) else 1)'
	@rm -rf $@
	@($(MAKE_VENV) $@ && $@/bin/pip3 install -U 'pip >= 19.0.0' && $@/bin/pip install -r $<) || rm -rf $@

$(SPHINXBUILD): $(VENV)

.PHONY: print_versions
print_versions: $(VENV)
	$(VENV)/bin/pip3 freeze

# Catch-all target: route all unknown targets to Sphinx using the new
# "make mode" option.  $(O) is meant as a shortcut for $(SPHINXOPTS).
%: $(SPHINXBUILD) Makefile
	@$(SPHINXBUILD) "$(SOURCEDIR)" "$(BUILDDIR)" $(SPHINXOPTS) $(O)
