PORTNAME=	atf
DISTVERSION=	0.22
PORTREVISION=	1
CATEGORIES=	devel
MASTER_SITES=	https://github.com/freebsd/${PORTNAME}/releases/download/${PORTNAME}-${DISTVERSION}/

PATCH_SITES=	https://github.com/freebsd/${PORTNAME}/commit/
PATCHFILES=	b42c98612cb99fa3f52766a46203263dc1de7187.patch:-p1

MAINTAINER=	bofh@FreeBSD.org
COMMENT=	C, C++ and shell libraries to write ATF-compliant test programs
WWW=		https://github.com/freebsd/atf

LICENSE=	BSD3CLAUSE

USES=		autoreconf libtool pathfix
USE_CXXSTD=	gnu++11
USE_LDCONFIG=	yes

GNU_CONFIGURE=	yes

INSTALL_TARGET=	install-strip

NO_WRKSUBDIR=	yes

OPTIONS_DEFINE=	DOCS TEST
OPTIONS_DEFAULT=TEST
OPTIONS_SUB=	yes

DOCS_MAKE_ARGS_OFF=	doc_DATA=

post-install-TEST-off:
	@${RM} -r ${STAGEDIR}${PREFIX}/tests

.include <bsd.port.mk>
