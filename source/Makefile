# $Id$
# public domain.  Originally written by Karl Berry.

default:
	@echo "make build to rebuild completely,"
	@echo "make remake to make the binary,"
	@echo "make versionhelp to see built --version and --help."
	@echo "make synctest or syncreal to sync with TL,"
	@echo "  and make svnstatus for file lists to help with syncing." 
	@echo "But read/understand the scripts before doing anything."

# full build.
build:
	./build-pdftex.sh
#
# just remake binary; we can build only pdftex in our stripped-down-tree.
remake:
	make -C build-pdftex/texk/web2c pdftex

# simple check that binary works.
versionhelp:
	cd build-pdftex/texk/web2c && ./pdftex --version && ./pdftex --help
#
# full make check, painful because the cut-down tree means we have to
# remove all dependencies (= we can't build the other engines).
# The list might change in the future with Makefile or automake changes.
recheck:
	make -C build-pdftex/texk/web2c TESTS='$$(pdftex_tests)' \
	  SUBDIRS=. PROGRAMS="" LIBRARIES="" LTLIBRARIES="" \
	  MANS="" DATA="" HEADERS="" \
	  check

synctest:
	svn status	  # if not clean, commit first or changes will be lost
	# also svn update the TL source dir, and note revision.
	./sync-pdftex.sh  # does not actually change anything.

syncreal:
	./sync-pdftex.sh --real | tee /tmp/pdfsync.out # read trailing info!
	$(MAKE) svnstatus

# The idea is to run this, do the needed svn adds and svn removes,
# then (if something fails, which usually happens), deal with it, then
# rerun this.  Repeat until all files are empty.
svnstatus:
	svn status >/tmp/sat
	-grep -v '^[MDA?!]' /tmp/sat >/tmp/sun # unknown
	ls -l /tmp/sun
	@echo
	sed -n 's/^\?//p'   /tmp/sat >/tmp/sad # add these
	ls -l /tmp/sad
	@echo
	sed -n 's/^!//p'    /tmp/sat >/tmp/srm # remove these
	ls -l /tmp/srm

# Commit after sync:
# tlrev=66599 # svnversion Build/source
# yy=`date +%Y`
# echo scom -m"\"sync from tl $tlrev, tl$YY release\"" # or just sync
# !*
# 
# # after release, making branch:
# prev=906   # from above
# pver=`pdftex --version | sed 1q | awk '{print $2}' | sed 's/.*-//'`
# echo $pver
#echo svn copy -r $prev \
# -m"\"pdftex $pver tag based on r$prev, tl$yy r$tlrev\"" \
# svn://tug.org/pdftex/branches/stable \
# svn://tug.org/pdftex/tags/pdftex-$pver
# !*
