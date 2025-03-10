PORTNAME=	librewolf
DISTVERSION=	134.0
DISTVERSIONSUFFIX=	-1.source
PORTREVISION=	1
CATEGORIES=	www wayland
MASTER_SITES=	https://gitlab.com/api/v4/projects/32320088/packages/generic/${PORTNAME}-source/${DISTVERSION}-1/

MAINTAINER=	freebsd@sysctl.cz
COMMENT=	Custom version of Firefox, focused on privacy, security and freedom
WWW=		https://librewolf.net/

LICENSE=	MPL20
LICENSE_FILE=	${WRKSRC}/LICENSE

BROKEN_armv7=	error: could not compile `gkrust` (lib)

BUILD_DEPENDS=	nspr>=4.32:devel/nspr \
		nss>=3.106:security/nss \
		icu>=73.1:devel/icu \
		libevent>=2.1.8:devel/libevent \
		harfbuzz>=10.0.1:print/harfbuzz \
		graphite2>=1.3.14:graphics/graphite2 \
		png>=1.6.44:graphics/png \
		dav1d>=1.0.0:multimedia/dav1d \
		libvpx>=1.14.1:multimedia/libvpx \
		${PYTHON_PKGNAMEPREFIX}sqlite3>0:databases/py-sqlite3@${PY_FLAVOR} \
		v4l_compat>0:multimedia/v4l_compat \
		autoconf2.13:devel/autoconf2.13 \
		nasm:devel/nasm \
		yasm:devel/yasm \
		zip:archivers/zip

USE_GECKO=	gecko
USE_MOZILLA=	-sqlite

# work around bindgen not finding ICU, e.g.
# dist/include/mozilla/intl/ICU4CGlue.h:8:10: fatal error: 'unicode/uenum.h' file not found, err: true
CONFIGURE_ENV+=	BINDGEN_CFLAGS="-I${LOCALBASE}/include"
CONFIGURE_ENV+=	MOZ_REQUIRE_SIGNING=""
CFLAGS_powerpc64le=	-DSQLITE_BYTEORDER=1234

WRKSRC=		${WRKDIR}/${PORTNAME}-${DISTVERSION}-1

MOZILLA_CAP=	${MOZILLA:C/^(.).*/\1/:tu}${MOZILLA:C/^.//}

MOZ_EXPORT+=	MOZ_TELEMETRY_REPORTING="" \
		MOZILLA_OFFICIAL="1" \
		MOZ_OFFICIAL_BRANDING="1" \
		MOZ_APP_DISPLAYNAME="${MOZILLA_CAP}" \
		MOZ_APP_NAME="${MOZILLA}"

MOZ_OPTIONS=	--enable-application=browser \
		--allow-addon-sideload \
		--disable-crashreporter \
		--disable-debug \
		--disable-default-browser-agent \
		--disable-tests \
		--disable-updater \
		--enable-hardening \
		--enable-optimize \
		--enable-release \
		--with-app-name=${MOZILLA} \
		--with-branding=browser/branding/${MOZILLA} \
		--with-unsigned-addon-scopes=app,system \
		--enable-bootstrap \
		MOZ_CRASHREPORTER=0 \
		MOZ_DATA_REPORTING=0

FIREFOX_ICON=		${MOZILLA}.png
FIREFOX_ICON_SRC=	${PREFIX}/lib/${MOZILLA}/browser/chrome/icons/default/default48.png

.include "${.CURDIR}/../../www/firefox/Makefile.options"

.include <bsd.port.options.mk>

.if ${ARCH} == amd64
MOZ_OPTIONS+=	--enable-rust-simd
.endif

.if ${ARCH} == powerpc64
CFLAGS+=	-DHWY_COMPILE_ONLY_SCALAR
MOZ_OPTIONS+=	--without-wasm-sandboxed-libraries
.else
BUILD_DEPENDS+=	${LOCALBASE}/share/wasi-sysroot/lib/wasm32-wasi/libc++abi.a:devel/wasi-libcxx${LLVM_VERSION} \
		${LOCALBASE}/share/wasi-sysroot/lib/wasm32-wasi/libc.a:devel/wasi-libc@${LLVM_VERSION} \
		wasi-compiler-rt${LLVM_VERSION}>0:devel/wasi-compiler-rt${LLVM_VERSION}
MOZ_OPTIONS+=	--with-wasi-sysroot=${LOCALBASE}/share/wasi-sysroot
.endif

post-extract:
	@${SED} -e 's|@FIREFOX_ICON@|${FIREFOX_ICON:R}|;s|@MOZILLA@|${MOZILLA}|' \
		-e 's|firefox|${MOZILLA}|' \
		-e 's|Firefox|${MOZILLA_CAP}|' \
		<${.CURDIR}/../firefox/files/firefox.desktop.in >${WRKDIR}/${MOZILLA_EXEC_NAME}.desktop

post-patch:
	@${REINPLACE_CMD} -e 's|%%LOCALBASE%%|${LOCALBASE}|g' \
		${WRKSRC}/browser/app/nsBrowserApp.cpp
	@${RM} ${WRKSRC}/mozconfig

post-install:
	${INSTALL_DATA} ${WRKDIR}/${MOZILLA_EXEC_NAME}.desktop ${STAGEDIR}${PREFIX}/share/applications
	${MKDIR} ${STAGEDIR}${PREFIX}/share/pixmaps
	${LN} -sf ${FIREFOX_ICON_SRC} ${STAGEDIR}${PREFIX}/share/pixmaps/${FIREFOX_ICON}

.include <bsd.port.mk>
