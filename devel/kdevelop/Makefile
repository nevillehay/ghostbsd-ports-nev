# When updating this port, also chase
#  devel/kdev-php
#  devel/kdev-python
PORTNAME=	kdevelop
DISTVERSION=	${KDE_APPLICATIONS_VERSION}
PORTREVISION=	4
CATEGORIES=	devel kde kde-applications

MAINTAINER=	kde@FreeBSD.org
COMMENT=	Plugin extensible IDE for C/C++ and other languages
WWW=		https://www.kdevelop.org/

LICENSE=	GPLv2+ LGPL20+
LICENSE_COMB=	multi

BUILD_DEPENDS=	kdev-pg-qt:devel/kdevelop-pg-qt
LIB_DEPENDS=	libKasten4Controllers.so:devel/okteta \
		libapr-1.so:devel/apr1 \
		libboost_thread.so:devel/boost-libs \
		libkomparediff2.so:textproc/libkomparediff2
.if ${WITH_SUBVERSION_VER:U} == LTS
LIB_DEPENDS+=	libsvn_client-1.so:devel/subversion-lts
.else
LIB_DEPENDS+=	libsvn_client-1.so:devel/subversion
.endif
RUN_DEPENDS=	gmake:devel/gmake

USES=		cmake compiler:c++11-lib desktop-file-utils gettext grantlee:5 \
		kde:5 llvm:build,run,noexport pkgconfig qt:5 shared-mime-info \
		shebangfix tar:xz xorg
USE_KDE=	archive attica auth bookmarks codecs completion config \
		configwidgets coreaddons crash emoticons guiaddons i18n \
		iconthemes init itemmodels itemviews jobwidgets kcmutils \
		kdeclarative kio libksysguard newstuff notifications \
		notifyconfig package parts plasma-framework purpose runner \
		service solid sonnet syntaxhighlighting texteditor textwidgets \
		threadweaver widgetsaddons windowsystem xmlgui
USE_QT=		concurrent core dbus declarative gui help location network \
		printsupport script sql webchannel webengine widgets xml \
		buildtools:build qmake:build
USE_XORG=	x11
SHEBANG_FILES=	kdevplatform/util/kdevplatform_shell_environment.sh \
		kdevplatform/util/.zshrc
# Most ports have ecm:build, testlib:build, but because this is an
# IDE, which **probably** is used for Qt / KDE development (also
# other things, but let's guess a target market), pull in some
# additional development things that are otherwise build-dep-only.
USE_KDE+=	ecm:build
USE_QT+=	testlib

CMAKE_ARGS=	-DCMAKE_POLICY_DEFAULT_CMP0074=NEW \
		-DClang_DIR=${LLVM_PREFIX}/lib/cmake/clang

# Versioning values, to reduce plist churn
SO_VER=		512
SO_VER_LONG=	5.12.230804
PLIST_SUB+=	SO_VER=${SO_VER} SO_VER_LONG=${SO_VER_LONG}

SHEBANG_LANG=	zsh
zsh_OLD_CMD=	/bin/zsh
zsh_CMD=	${LOCALBASE}/bin/zsh

.include <bsd.port.mk>
