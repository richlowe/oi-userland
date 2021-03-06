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
# Copyright 2017 Jason Martin
#

include ../../../make-rules/shared-macros.mk

COMPONENT_NAME=		gnumeric
COMPONENT_VERSION=	1.12.35
COMPONENT_PROJECT_URL=	http://www.gnome.org
COMPONENT_SUMMARY=	GTK Spreadsheet Application 
COMPONENT_SRC=		$(COMPONENT_NAME)-$(COMPONENT_VERSION)
COMPONENT_ARCHIVE=	$(COMPONENT_SRC).tar.xz
COMPONENT_ARCHIVE_HASH=	\
    sha256:77b1e3ce523578a807767ad71680fb865ac021d7bfadf93eada99ae094c06c0a
COMPONENT_ARCHIVE_URL=	http://ftp.gnome.org/pub/GNOME/sources/$(COMPONENT_NAME)/1.12/$(COMPONENT_ARCHIVE)
COMPONENT_FMRI=		desktop/$(COMPONENT_NAME)
COMPONENT_CLASSIFICATION=	Applications/Office
COMPONENT_LICENSE= GPLv2
COMPONENT_LICENSE_FILE= COPYING

include $(WS_MAKE_RULES)/prep.mk
include $(WS_MAKE_RULES)/configure.mk
include $(WS_MAKE_RULES)/ips.mk

PATH=$(PATH.gnu)

CONFIGURE_BINDIR.64 = $(CONFIGURE_BINDIR.32)

CONFIGURE_OPTIONS+=	--sysconfdir=/etc
CONFIGURE_OPTIONS+=	--libexecdir=$(CONFIGURE_LIBDIR.$(BITS))
CONFIGURE_OPTIONS+=	--without-perl

CONFIGURE_ENV+= PYTHON=$(PYTHON)

# common targets
build:		$(BUILD_64)

install:	$(INSTALL_64)

# To prevent "libtool_install_magic: unbound variable"
unexport SHELLOPTS

# All PASS or SKIP unless valgrind installed 08.26.2017
test:		$(TEST_64)

REQUIRED_PACKAGES += library/desktop/atk
REQUIRED_PACKAGES += library/desktop/cairo
REQUIRED_PACKAGES += library/desktop/gdk-pixbuf
REQUIRED_PACKAGES += library/desktop/goffice
REQUIRED_PACKAGES += library/desktop/gtk3
REQUIRED_PACKAGES += library/desktop/libgsf
REQUIRED_PACKAGES += library/desktop/pango
REQUIRED_PACKAGES += library/glib2
REQUIRED_PACKAGES += library/libxml2
REQUIRED_PACKAGES += library/zlib
REQUIRED_PACKAGES += runtime/python-27
REQUIRED_PACKAGES += system/library
REQUIRED_PACKAGES += system/library/math
