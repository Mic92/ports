# Created by: Sergei Kolobov <sergei@kolobov.com>
# $FreeBSD: head/devel/skalibs/Makefile 360487 2014-07-03 23:57:07Z adamw $

PORTNAME=	s6
PORTVERSION=	2.1.0.1
CATEGORIES=	sysutils
MASTER_SITES=	http://www.skarnet.org/software/${PORTNAME}/

MAINTAINER=	colin@heliocat.net
COMMENT=	skarnet.org supervision suite

LICENSE=	ISCL

BUILD_DEPENDS=	skalibs>=2.2.1.0:${PORTSDIR}/devel/skalibs \
		execline>=2.0.2.0:${PORTSDIR}/lang/execline
RUN_DEPENDS=	execlineb:${PORTSDIR}/lang/execline

USES=		gmake
USE_RC_SUBR=	s6
SERVICE_DIR?=	/var/service
SUB_LIST=	SERVICE_DIR="${SERVICE_DIR}"

DOCS=		AUTHORS COPYING INSTALL README doc/*.html

USE_LDCONFIG=	yes
HAS_CONFIGURE=	yes
CONFIGURE_ARGS+=--prefix=${PREFIX} \
	--with-sysdeps=${LOCALBASE}/lib/skalibs/sysdeps \
	--with-include=${LOCALBASE}/include \
	--with-lib=${LOCALBASE}/lib/skalibs \
	--with-lib=${LOCALBASE}/lib/execline \
	--enable-shared

post-install:
.for f in ${STAGEDIR}${PREFIX}/bin/* ${STAGEDIR}${PREFIX}/sbin/*
	${STRIP_CMD} ${STAGEDIR}${PREFIX}${f}
.endfor
	${STRIP_CMD} ${STAGEDIR}${PREFIX}/lib/libs6.so.${PORTVERSION}
	${STRIP_CMD} ${STAGEDIR}${PREFIX}/libexec/s6lockd-helper
	@${MKDIR} ${STAGEDIR}${DOCSDIR}
	cd ${WRKSRC} && ${INSTALL_MAN} ${DOCS} ${STAGEDIR}${DOCSDIR}
	cd ${WRKSRC} && ${INSTALL_SCRIPT} examples/s6-svscanboot \
		${STAGEDIR}${PREFIX}/bin
	@${MKDIR} ${STAGEDIR}${ETCDIR}/s6-svscan/env
	cd ${WRKSRC}/examples/.s6-svscan && ${INSTALL_SCRIPT} finish \
		${STAGEDIR}${ETCDIR}/s6-svscan/finish.sample
	cd ${WRKSRC}/examples/.s6-svscan/env && ${INSTALL_DATA} PATH \
		${STAGEDIR}${ETCDIR}/s6-svscan/env/PATH.sample
	@${MKDIR} ${STAGEDIR}${ETCDIR}/s6-svscan-log
	cd ${WRKSRC}/examples/ROOT/img/tmpfs/service/s6-svscan-log && \
		${INSTALL_SCRIPT} run ${STAGEDIR}${ETCDIR}/s6-svscan-log/run.sample

.include <bsd.port.mk>
