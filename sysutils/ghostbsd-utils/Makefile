PORTNAME=	ghostbsd-utils
PORTVERSION=	24.01.1
PORTREVISION=	0
CATEGORIES=	sysutils

MAINTAINER=	eturgeon@ixsystems.com
COMMENT=	GhostBSD util tools

USES=		metaport

RUN_DEPENDS=	update-station:ports-mgmt/update-station \
		backup-station:sysutils/backup-station \
		sudo:security/sudo \
		setxkbmap:x11/setxkbmap \
		xmodmap:x11/xmodmap \
		xdg-user-dirs-update:devel/xdg-user-dirs \
		networkmgr:net-mgmt/networkmgr \
		software-station:ports-mgmt/software-station \
		fish:shells/fish \
		webcamd:multimedia/webcamd

.include <bsd.port.mk>
