PORTNAME=	kcfonts
PORTVERSION=	1.05
PORTREVISION=	4
CATEGORIES=	chinese x11-fonts
MASTER_SITES=	GENTOO

MAINTAINER=	ports@FreeBSD.org
COMMENT=	Kuo Chauo Chinese Fonts collection

DEPRECATED=	GENTOO MASTER_SITES are no longer available
EXPIRATION_DATE=2025-01-27

BUILD_DEPENDS=	bdftopcf:x11-fonts/bdftopcf

USES=		fonts

MAKE_ARGS=	CFONTDIR=${FONTSDIR} EFONTDIR=${FONTSDIR}
MAKE_JOBS_UNSAFE=yes

NO_WRKSUBDIR=	yes

pre-install:
	${MKDIR} ${STAGEDIR}${FONTSDIR}

.include <bsd.port.mk>
