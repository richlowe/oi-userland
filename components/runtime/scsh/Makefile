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

COMPONENT_NAME=		scsh
COMPONENT_VERSION=	0.6.7
COMPONENT_SUMMARY=	The Scheme Shell
COMPONENT_PROJECT_URL=	http://scsh.net
COMPONENT_FMRI=		runtime/scsh
COMPONENT_CLASSIFICATION=Development/Other Languages
COMPONENT_SRC=		scsh-$(COMPONENT_VERSION)
COMPONENT_ARCHIVE=	$(COMPONENT_SRC).tar.gz
COMPONENT_ARCHIVE_HASH=	\
  sha256:c4a9f7df2a0bb7a7aa3dafc918aa9e9a566d4ad33a55f0192889de172d1ddb7f
COMPONENT_ARCHIVE_URL= \
  http://ftp.scsh.net/pub/scsh/0.6/$(COMPONENT_ARCHIVE)

COMPONENT_LICENSE=	BSD

include $(WS_MAKE_RULES)/prep.mk
include $(WS_MAKE_RULES)/configure.mk
include $(WS_MAKE_RULES)/ips.mk

PATH=$(PATH.gnu)

build:		$(BUILD_32)

install:	$(INSTALL_32)

test:		$(TEST_32)

# Auto-generated dependencies
REQUIRED_PACKAGES += system/library
REQUIRED_PACKAGES += system/library/math
