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
PREFERRED_BITS=64

include ../../../make-rules/shared-macros.mk

COMPONENT_NAME=		chibi-scheme
COMPONENT_VERSION=	0.8
COMPONENT_SUMMARY=	Chibi Scheme
COMPONENT_PROJECT_URL=	http://github.com/ashinn/chibi-scheme
COMPONENT_FMRI=		runtime/chibi-scheme
COMPONENT_CLASSIFICATION=Development/Other Languages
COMPONENT_SRC=		$(COMPONENT_NAME)-$(COMPONENT_VERSION)
COMPONENT_ARCHIVE=	$(COMPONENT_SRC).tar.gz
COMPONENT_ARCHIVE_HASH=	\
  sha256:8a077859b123216c123c243db391b0fe4c0cf73978c7cdd7b8ea853a48192756
COMPONENT_ARCHIVE_URL= \
  https://github.com/ashinn/chibi-scheme/archive/$(COMPONENT_VERSION).tar.gz
COMPONENT_LICENSE=	BSD

include $(WS_MAKE_RULES)/prep.mk
include $(WS_MAKE_RULES)/justmake.mk
include $(WS_MAKE_RULES)/ips.mk

COMPONENT_PRE_BUILD_ACTION= ($(CLONEY) $(SOURCE_DIR) $(@D))
COMPONENT_BUILD_ARGS += CC="$(CC)" PREFIX=/usr

COMPONENT_INSTALL_ARGS +=	PREFIX=/usr
COMPONENT_TEST_TARGETS= test

build:		$(BUILD_32)

install:	$(INSTALL_32)

test:		$(TEST_32)

# Auto-generated dependencies
REQUIRED_PACKAGES = SUNWcs
REQUIRED_PACKAGES += system/library
REQUIRED_PACKAGES += system/library/math
