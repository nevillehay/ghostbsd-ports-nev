PORTNAME=	mopac
DISTVERSIONPREFIX=	v
DISTVERSION=	23.0.3
PORTEPOCH=	1
CATEGORIES=	science # chemistry

MAINTAINER=	yuri@FreeBSD.org
COMMENT=	Semi-empirical (MNDO, etc.) molecular orbital calculation
WWW=		http://openmopac.net/

LICENSE=	GPLv3
LICENSE_FILE=	${WRKSRC}/COPYING

TEST_DEPENDS=	${PYNUMPY}

USES=		blaslapack:openblas cmake:testing fortran python:test
USE_LDCONFIG=	yes

USE_GITHUB=	yes
GH_ACCOUNT=	openmopac

CMAKE_OFF=	TESTS
CMAKE_TESTING_ON=	TESTS # all tests pass
CMAKE_ARGS=	-DPython3_EXECUTABLE=${PYTHON_CMD} #-DPython3_NumPy_INCLUDE_DIRS=${PYTHONPREFIX_SITELIBDIR}/numpy/core/include

PLIST_FILES=	bin/mopac \
		bin/mopac-makpol \
		bin/mopac-param \
		include/mopac.h \
		lib/libmopac.so \
		lib/libmopac.so.2

.include <bsd.port.mk>
