PORTNAME=	datadog
PORTVERSION=	2.8.0
CATEGORIES=	devel rubygems
MASTER_SITES=	RG

MAINTAINER=	sunpoet@FreeBSD.org
COMMENT=	Datadog's client library for Ruby
WWW=		https://github.com/DataDog/dd-trace-rb

LICENSE=	APACHE20 BSD3CLAUSE
LICENSE_COMB=	dual
LICENSE_FILE_APACHE20=	${WRKSRC}/LICENSE.Apache
LICENSE_FILE_BSD3CLAUSE=${WRKSRC}/LICENSE.BSD3

RUN_DEPENDS=	rubygem-datadog-ruby_core_source>=3.3<4:devel/rubygem-datadog-ruby_core_source \
		rubygem-libdatadog>=14.3.1.1.0<14.3.1.2:devel/rubygem-libdatadog \
		rubygem-libddwaf>=1.18.0.0.0<1.18.0.1:devel/rubygem-libddwaf \
		rubygem-msgpack>=0:devel/rubygem-msgpack

USES=		gem

PLIST_FILES=	bin/ddprofrb

.include <bsd.port.mk>
