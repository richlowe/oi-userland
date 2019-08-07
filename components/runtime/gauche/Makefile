#
# This file and its contents are supplied under the terms of the
# Common Development and Distribution License ("CDDL"), version 1.0.
# You may only use this file in accordance with the terms of version
# 1.0 of the CDDL.
#
# A full copy of the text of the CDDL should have accompanied this
# source.  A copy of the CDDL is also available via the Internet at
# http://www.illumos.org/license/CDDL.
#

#
# Copyright 2019 Richard Lowe
#
include ../../../make-rules/shared-macros.mk

COMPONENT_NAME=		gauche
COMPONENT_VERSION=	0.9.8
COMPONENT_SUMMARY=	Gauche Scheme
COMPONENT_PROJECT_URL=	https://practical-scheme.net/gauche/
COMPONENT_FMRI=		runtime/gauche
COMPONENT_CLASSIFICATION=Development/Other Languages
COMPONENT_SRC=		Gauche-$(COMPONENT_VERSION)
COMPONENT_ARCHIVE=	$(COMPONENT_SRC).tar.gz
COMPONENT_ARCHIVE_HASH=	\
  sha256:3eb30d1051d8b48999fe46511c9f6983057735312c9832b7db13f9db140db74b
COMPONENT_ARCHIVE_URL= \
  http://prdownloads.sourceforge.net/gauche/Gauche-0.9.8.tgz
COMPONENT_LICENSE=	BSD

include $(WS_MAKE_RULES)/prep.mk
include $(WS_MAKE_RULES)/configure.mk
include $(WS_MAKE_RULES)/ips.mk

COMPONENT_TEST_TARGETS= test
#COMPONENT_PRE_CONFIGURE_ACTION= ($(CLONEY) $(SOURCE_DIR) $(@D))

#CONFIGURE_ENV = CONFIG_SHELL="$(CONFIG_SHELL)"
CONFIGURE_ENV =
CONFIGURE_ENV += CC="$(CC)"
CONFIGURE_ENV += CXX="$(CXX)"
CONFIGURE_ENV += F77="$(F77)"
CONFIGURE_ENV += FC="$(FC)"
CONFIGURE_ENV += CFLAGS="$(CFLAGS)"
CONFIGURE_ENV += CXXFLAGS="$(CXXFLAGS)"
CONFIGURE_ENV += FFLAGS="$(F77FLAGS)"
CONFIGURE_ENV += FCFLAGS="$(FCFLAGS)"
CONFIGURE_ENV += LDFLAGS="$(LDFLAGS)"
CONFIGURE_ENV += PKG_CONFIG_PATH="$(PKG_CONFIG_PATH)"

build:		$(BUILD_32)

install:	$(INSTALL_32)

test:		$(TEST_32)

# Auto-generated dependencies
REQUIRED_PACKAGES = library/database/gdbm
REQUIRED_PACKAGES += library/zlib
REQUIRED_PACKAGES += system/library
REQUIRED_PACKAGES += system/library/math
