COMMENT=	maildir indexer and searcher with emacs frontend

V=		1.8.14
GUILE_V=	3.0

DISTNAME=	mu-$V

FLAVORS=	guile
FLAVOR ?=

SHARED_LIBS=	guile-mu	0.0

CATEGORIES=	mail
HOMEPAGE=	http://www.djcbsoftware.nl/code/mu/

MAINTAINER=	Stefan Hagen <sh+ports@codevoid.de>

# GPLv3+
PERMIT_PACKAGE=	Yes

WANTLIB += ${COMPILER_LIBCXX} assuan c curses ffi gio-2.0 glib-2.0
WANTLIB += gmime-3.0 gmodule-2.0 gobject-2.0 gpg-error gpgme
WANTLIB += gthread-2.0 iconv idn2 intl m pcre2-8 unistring
WANTLIB += xapian z

MASTER_SITES=	https://github.com/djcb/mu/releases/download/v${V}/
EXTRACT_SUFX=	.tar.xz

MODULES=		devel/meson

BUILD_DEPENDS=	emacs->=26.3:editors/emacs

LIB_DEPENDS=	databases/xapian-core \
		devel/glib2 \
		mail/gmime30 \
		security/gpgme

# C++17
COMPILER=	base-clang ports-gcc

.if ${FLAVOR} == "guile"
WANTLIB +=		guile-${GUILE_V} gc ltdl gmp
LIB_DEPENDS +=		devel/libtool,-ltdl \
			lang/guile3
.else
CONFIGURE_ARGS +=	-Dguile=disabled
.endif

# needs readline >= 8.0
CONFIGURE_ARGS +=	-Dreadline=disabled

pre-configure:
	sed -e 's/exec guile/exec guile${GUILE_V}/' -i \
		${WRKDIST}/guile/*/*.scm
	sed -e 's/guile-snarf/guile-snarf${GUILE_V}/' -i \
		${WRKDIST}/configure.ac

.include <bsd.port.mk>
