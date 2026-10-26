# $Id$
# Public domain. Originally written by Karl Berry.
# Top-level tests Makefile.

default:
	@echo "install to copy tests to TL Master for distribution."
	@echo "all to try running all tests, but doesn't work."

all:
	for d in *; do make -C $$d </dev/null || exit 1; done >log 2>&1

dest = /home/texlive/karl/Master/texmf-dist/doc/pdftex/tests
filelist = /tmp/sat # svn status, numbers, not directories or .
$(filelist) filelist: Makefile
	svn status -v | cut -c 42- | grep / >$(filelist)
install: $(filelist)
	rsync -avRL `cat $(filelist)` $(dest)/
	# then run the svn commands to add as needed.
