# Created by: Kevin Lo <kevlo@FreeBSD.org>
# $FreeBSD$

PORTNAME=	owncloud
PORTVERSION=	10.0.6
CATEGORIES=	www
MASTER_SITES=	http://download.owncloud.org/community/

MAINTAINER=	sunpoet@FreeBSD.org
COMMENT=	Personal cloud which runs on your own server

LICENSE=	AGPLv3
LICENSE_FILE=	${WRKSRC}/COPYING

USES=		cpe tar:bzip2 php:web
USE_PHP=	bz2 ctype curl dom fileinfo filter gd hash iconv intl json \
		mbstring pdo posix session simplexml xml xmlreader xmlwriter \
		xsl wddx zip zlib

OWNCLOUD_USERNAME?=	${WWWOWN}
OWNCLOUD_GROUPNAME?=	${WWWGRP}

WRKSRC=		${WRKDIR}/${PORTNAME}
NO_BUILD=	yes
NO_ARCH=	yes
SUB_FILES=	pkg-message newsyslog
PLIST_SUB=	OWNCLOUD_USERNAME=${OWNCLOUD_USERNAME} \
		OWNCLOUD_GROUPNAME=${OWNCLOUD_GROUPNAME}

OPTIONS_DEFINE=	EXAMPLES EXIF LDAP SMB SSL
OPTIONS_MULTI=	DB
OPTIONS_MULTI_DB=	MYSQL PGSQL SQLITE
OPTIONS_DEFAULT=EXIF LDAP MYSQL SMB SSL

EXIF_DESC=	Image rotation support

EXIF_USE=	PHP=exif
LDAP_USE=	PHP=ldap
MYSQL_USE=	PHP=pdo_mysql
MYSQL_USES=	mysql
PGSQL_USES=	pgsql
PGSQL_USE=	PHP=pdo_pgsql,pgsql
SQLITE_USE=	PHP=pdo_sqlite,sqlite3
SMB_RUN_DEPENDS=	pecl-smbclient>=0.8.0:net/pecl-smbclient
SSL_USE=	PHP=openssl

do-install:
	${MKDIR} ${STAGEDIR}${PREFIX}/etc/newsyslog.conf.d/
	${MKDIR} -m 0755 ${STAGEDIR}${WWWDIR}/
	cd ${WRKSRC} && ${COPYTREE_SHARE} . ${STAGEDIR}${WWWDIR}
	${MKDIR} ${STAGEDIR}${WWWDIR}/data

do-install-EXAMPLES-on:
	${MKDIR} ${STAGEDIR}${EXAMPLESDIR}/
	${INSTALL_DATA} ${WRKDIR}/newsyslog ${STAGEDIR}${EXAMPLESDIR}

.include <bsd.port.mk>
