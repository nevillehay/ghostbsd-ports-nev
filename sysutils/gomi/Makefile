PORTNAME=	gomi
DISTVERSIONPREFIX=	v
DISTVERSION=	1.1.8
PORTREVISION=	1
CATEGORIES=	sysutils

MAINTAINER=	eduardo@FreeBSD.org
COMMENT=	Unix rm(1) command that can restore deleted files
WWW=		https://github.com/b4b4r07/gomi

LICENSE=	MIT
LICENSE_FILE=	${WRKSRC}/LICENSE

USES=		go:1.23,modules

_BUILD_VERSION=		${DISTVERSIONFULL}
_BUILD_REVISION=	01c4325

GO_MODULE=	github.com/b4b4r07/gomi
GO_BUILDFLAGS=	-ldflags "\
		-s -w \
		-X main.Version=${_BUILD_VERSION} \
		-X main.Revision=${_BUILD_REVISION}"

PLIST_FILES=	bin/${PORTNAME}
PORTDOCS=	README.md

OPTIONS_DEFINE=	DOCS

post-install-DOCS-on:
	@${MKDIR} ${STAGEDIR}${DOCSDIR}
	${INSTALL_DATA} ${PORTDOCS:S,^,${WRKSRC}/,} ${STAGEDIR}${DOCSDIR}

.include <bsd.port.mk>
