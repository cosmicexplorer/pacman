SUBDIRS = po

EXTRA_DIST = meson.build po/meson.build

# paths set at make time
conffile  = ${sysconfdir}/pacman.conf
dbpath    = ${localstatedir}/lib/pacman/
gpgdir    = ${sysconfdir}/pacman.d/gnupg/
hookdir   = ${sysconfdir}/pacman.d/hooks/
cachedir  = ${localstatedir}/cache/pacman/pkg/
logfile   = ${localstatedir}/log/pacman.log

noinst_LTLIBRARIES = \
	libbasic.la

libbasic_la_SOURCES = \
	conf.h conf.c \
	ini.h ini.c \
	callback.h callback.c \
	util.h util.c \
	util-common.h util-common.c

libbasic_la_LIBADD = \
	$(top_builddir)/lib/libalpm/.libs/libalpm.la

bin_PROGRAMS = pacman pacman-conf

AM_CPPFLAGS = \
	-imacros $(top_builddir)/config.h \
	-I$(top_srcdir)/lib/libalpm \
	-DLOCALEDIR=\"@localedir@\" \
	-DCONFFILE=\"$(conffile)\" \
	-DDBPATH=\"$(dbpath)\" \
	-DGPGDIR=\"$(gpgdir)\" \
	-DHOOKDIR=\"$(hookdir)\" \
	-DCACHEDIR=\"$(cachedir)\" \
	-DLOGFILE=\"$(logfile)\"

AM_CFLAGS = -pedantic -D_GNU_SOURCE $(WARNING_CFLAGS) \
	$(LIBARCHIVE_CFLAGS)

if USE_GIT_VERSION
GIT_VERSION := $(shell sh -c 'git describe --abbrev=4 --dirty | sed s/^v//')
AM_CPPFLAGS += -DGIT_VERSION=\"$(GIT_VERSION)\"
endif

pacman_SOURCES = \
	check.h check.c \
	database.c \
	deptest.c \
	files.c \
	package.h package.c \
	pacman.h pacman.c \
	query.c \
	remove.c \
	sighandler.h sighandler.c \
	sync.c \
	upgrade.c

pacman_LDADD = \
	$(LTLIBINTL) \
	libbasic.la \
	$(top_builddir)/lib/libalpm/.libs/libalpm.la \
	$(LIBARCHIVE_LIBS)

pacman_conf_SOURCES = pacman-conf.c

pacman_conf_LDADD = \
	libbasic.la \
	$(top_builddir)/lib/libalpm/.libs/libalpm.la
