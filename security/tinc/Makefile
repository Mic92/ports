# Created by: ijliao
# $FreeBSD: head/security/tinc/Makefile 362126 2014-07-17 08:57:51Z olgeni $

PORTNAME=	tinc
PORTVERSION=	1.1pre11
PORTREVISION=5
CATEGORIES=	security
MASTER_SITES=	http://www.tinc-vpn.org/packages/ \
	ftp://ftp.wiretapped.net/pub/security/network-security/tinc/ \
	http://www.mirrors.wiretapped.net/security/network-security/tinc/

MAINTAINER=	dinoex@FreeBSD.org
COMMENT=	Virtual Private Network (VPN) daemon

LIB_DEPENDS=	liblzo2.so:${PORTSDIR}/archivers/lzo2 \
	libreadline.6:${PORTSDIR}/devel/readline

LICENSE=	GPLv3

USES=		makeinfo
USE_OPENSSL=	yes
GNU_CONFIGURE=	yes
CPPFLAGS+=	-I${LOCALBASE}/include
LDFLAGS+=	-L${LOCALBASE}/lib
CONFIGURE_ARGS=	--localstatedir=/var
USE_RC_SUBR=	tincd
INFO=		tinc
PLIST_FILES=	sbin/tincd sbin/tinc \
	sbin/sptps_keypair sbin/sptps_test \
	man/man5/tinc.conf.5.gz man/man8/tincd.8.gz

.include <bsd.port.mk>
