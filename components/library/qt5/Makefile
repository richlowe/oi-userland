#
# This file and its contents are supplied under the terms of the
# Common Development and Distribution License ("CDDL)". You may
# only use this file in accordance with the terms of the CDDL.
#
# A full copy of the text of the CDDL should have accompanied this
# source. A copy of the CDDL is also available via the Internet at
# http://www.illumos.org/license/CDDL.
#

#
# Copyright 2014 EveryCity Ltd. All rights reserved.
# Copyright 2015 Alexander Pyhalov
# Copyright 2017 Aurelien Larcher
#

include ../../../make-rules/shared-macros.mk

COMPONENT_NAME=           qt
COMPONENT_VERSION=        5.8.0
COMPONENT_REVISION=       3
COMPONENT_VERSION_MJR=    5.8
COMPONENT_FMRI=           library/qt5
COMPONENT_PROJECT_URL=    https://www.qt.io/
COMPONENT_SUMMARY=        Qt cross-platform application and UI framework
COMPONENT_CLASSIFICATION= Desktop (GNOME)/Libraries
COMPONENT_SRC=		$(COMPONENT_NAME)-everywhere-opensource-src-$(COMPONENT_VERSION)
COMPONENT_ARCHIVE=	$(COMPONENT_SRC).tar.gz
COMPONENT_ARCHIVE_HASH=	\
  sha256:9dc5932307ae452855863f6405be1f7273d91173dcbe4257561676a599bd58d3
COMPONENT_ARCHIVE_URL=\
  http://download.qt.io/official_releases/qt/$(COMPONENT_VERSION_MJR)/$(COMPONENT_VERSION)/single/$(COMPONENT_ARCHIVE)
COMPONENT_LICENSE=        QT5
COMPONENT_LICENSE_FILE=   qt5.license

include $(WS_MAKE_RULES)/prep.mk
include $(WS_MAKE_RULES)/configure.mk
include $(WS_MAKE_RULES)/ips.mk

PATH=$(PG_BINDIR.$(BITS)):$(MYSQL_BINDIR.$(BITS)):/usr/gnu/bin:/usr/bin

QT_PREFIX=$(USRLIBDIR)/$(COMPONENT_NAME)/$(COMPONENT_VERSION_MJR)

QT_ARCHSUBDIR.32=
QT_ARCHSUBDIR.64=$(MACH64)
QT_PLATFORM.32= solaris-g++
QT_PLATFORM.64= solaris-g++-64

CONFIGURE_OPTIONS = -prefix $(QT_PREFIX)
CONFIGURE_OPTIONS+= -verbose
CONFIGURE_OPTIONS+= -opensource
CONFIGURE_OPTIONS+= -confirm-license
CONFIGURE_OPTIONS+= -nomake examples
CONFIGURE_OPTIONS+= -nomake tests
CONFIGURE_OPTIONS+= -c++std c++11
CONFIGURE_OPTIONS+= -disable-reduce-exports
CONFIGURE_OPTIONS+= -qt-xcb
CONFIGURE_OPTIONS+= -bindir $(QT_PREFIX)/bin/$(QT_ARCHSUBDIR.$(BITS))
CONFIGURE_OPTIONS+= -libdir $(QT_PREFIX)/lib/$(QT_ARCHSUBDIR.$(BITS))
CONFIGURE_OPTIONS+= -plugindir $(QT_PREFIX)/plugins/$(QT_ARCHSUBDIR.$(BITS))
CONFIGURE_OPTIONS+= -importdir $(QT_PREFIX)/imports/$(QT_ARCHSUBDIR.$(BITS))
CONFIGURE_OPTIONS+= -qmldir $(QT_PREFIX)/qml/$(QT_ARCHSUBDIR.$(BITS))
CONFIGURE_OPTIONS+= -platform $(QT_PLATFORM.$(BITS))
CONFIGURE_OPTIONS+= -plugin-sql-mysql
CONFIGURE_OPTIONS+= -plugin-sql-psql
CONFIGURE_OPTIONS+= -system-sqlite
CONFIGURE_OPTIONS+= $(CONFIGURE_OPTIONS.$(BITS))

COMPONENT_INSTALL_ENV+=	INSTALL_ROOT=$(PROTO_DIR)

# Set relative runpath to sql plugins
QT_LIBDIR    =$(QT_PREFIX)/lib/$(QT_ARCHSUBDIR.$(BITS))
QT_SQLDIR    =$(QT_PREFIX)/plugins/$(QT_ARCHSUBDIR.$(BITS))/sqldrivers
QT_QTSQLRPATH=$(shell realpath -m --relative-to=$(QT_SQLDIR) $(QT_LIBDIR))
QT_MYSQLRPATH=$(shell realpath -m --relative-to=$(QT_SQLDIR) $(MYSQL_LIBDIR.$(BITS)))
QT_PGSQLRPATH=$(shell realpath -m --relative-to=$(QT_SQLDIR) $(PG_LIBDIR.$(BITS)))
# Set relative runpath to eql plugins
QT_XORGDIR   =$(QT_PREFIX)/lib/xorg/$(QT_ARCHSUBDIR.$(BITS))
QT_EGLDIR    =$(QT_PREFIX)/plugins/$(QT_ARCHSUBDIR.$(BITS))/egldeviceintegrations
QT_QTEGLRPATH=$(shell realpath -m --relative-to=$(QT_EGLDIR) $(QT_LIBDIR))
QT_EGLSORPATH=$(shell realpath -m --relative-to=$(QT_EGLDIR) $(QT_XORGDIR))
# Set relative runpath to eql libraries
QT_DRMSORPATH=$(shell realpath -m --relative-to=$(QT_LIBDIR) $(QT_XORGDIR))

COMPONENT_POST_INSTALL_ACTION= ( \
/usr/bin/elfedit -e 'dyn:runpath "$$ORIGIN/$(QT_QTSQLRPATH):$$ORIGIN/$(QT_MYSQLRPATH)"' \
	$(PROTO_DIR)$(QT_SQLDIR)/libqsqlmysql.so; \
/usr/bin/elfedit -e 'dyn:runpath "$$ORIGIN/$(QT_QTSQLRPATH):$$ORIGIN/$(QT_PGSQLRPATH)"' \
	$(PROTO_DIR)$(QT_SQLDIR)/libqsqlpsql.so; \
/usr/bin/elfedit -e 'dyn:runpath "$$ORIGIN/$(QT_QTEGLRPATH):$$ORIGIN/$(QT_EGLSORPATH)"' \
	$(PROTO_DIR)$(QT_EGLDIR)/libqeglfs-kms-integration.so; \
/usr/bin/elfedit -e 'dyn:runpath "$$ORIGIN/$(QT_QTEGLRPATH):$$ORIGIN/$(QT_EGLSORPATH)"' \
	$(PROTO_DIR)$(QT_EGLDIR)/libqeglfs-kms-egldevice-integration.so; \
/usr/bin/elfedit -e 'dyn:runpath "$$ORIGIN:$$ORIGIN/$(QT_DRMSORPATH)"' \
	$(PROTO_DIR)$(QT_LIBDIR)/libQt5EglFsKmsSupport.so.$(COMPONENT_VERSION); \
)

build:		$(BUILD_32_and_64)

install:	$(INSTALL_32_and_64)

# Build dependencies
REQUIRED_PACKAGES += database/freetds
REQUIRED_PACKAGES += database/mariadb-101/client
REQUIRED_PACKAGES += database/postgres-94/developer
REQUIRED_PACKAGES += system/header/header-drm
REQUIRED_PACKAGES += x11/keyboard/data-xkb
REQUIRED_PACKAGES += x11/library/libpthread-stubs

# Auto-generated dependencies
REQUIRED_PACKAGES += codec/jasper
REQUIRED_PACKAGES += database/mariadb-101/library
REQUIRED_PACKAGES += database/postgres-94/library
REQUIRED_PACKAGES += database/sqlite-3
REQUIRED_PACKAGES += image/library/libjpeg6
REQUIRED_PACKAGES += image/library/libjpeg6-ijg
REQUIRED_PACKAGES += image/library/libpng16
REQUIRED_PACKAGES += image/library/libtiff
REQUIRED_PACKAGES += library/audio/gstreamer1
REQUIRED_PACKAGES += library/audio/gstreamer1/plugin/base
REQUIRED_PACKAGES += library/audio/openal
REQUIRED_PACKAGES += library/audio/pulseaudio
REQUIRED_PACKAGES += library/c++/harfbuzz
REQUIRED_PACKAGES += library/desktop/gtk3
REQUIRED_PACKAGES += library/desktop/pango
REQUIRED_PACKAGES += library/freetds
REQUIRED_PACKAGES += library/glib2
REQUIRED_PACKAGES += library/print/cups-libs
REQUIRED_PACKAGES += library/sdl2
REQUIRED_PACKAGES += library/zlib
REQUIRED_PACKAGES += system/library
REQUIRED_PACKAGES += system/library/fontconfig
REQUIRED_PACKAGES += system/library/freetype-2
REQUIRED_PACKAGES += system/library/g++-4-runtime
REQUIRED_PACKAGES += system/library/gcc-4-runtime
REQUIRED_PACKAGES += system/library/libdbus
REQUIRED_PACKAGES += system/library/math
REQUIRED_PACKAGES += text/hunspell
REQUIRED_PACKAGES += x11/library/libdrm
REQUIRED_PACKAGES += x11/library/libice
REQUIRED_PACKAGES += x11/library/libsm
REQUIRED_PACKAGES += x11/library/libx11
REQUIRED_PACKAGES += x11/library/libxcb
REQUIRED_PACKAGES += x11/library/libxi
REQUIRED_PACKAGES += x11/library/libxkbcommon
REQUIRED_PACKAGES += x11/library/mesa
