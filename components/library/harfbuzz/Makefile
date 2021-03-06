#
# CDDL HEADER START
#
# The contents of this file are subject to the terms of the
# Common Development and Distribution License (the "License").
# You may not use this file except in compliance with the License.
#
# You can obtain a copy of the license at usr/src/OPENSOLARIS.LICENSE
# or http://www.illumos.org/license/CDDL.
# See the License for the specific language governing permissions
# and limitations under the License.
#
# When distributing Covered Code, include this CDDL HEADER in each
# file and include the License file at usr/src/OPENSOLARIS.LICENSE.
# If applicable, add the following below this CDDL HEADER, with the
# fields enclosed by brackets "[]" replaced with your own identifying
# information: Portions Copyright [yyyy] [name of copyright owner]
#
# CDDL HEADER END
#
# Copyright (c) 2015-2018, Aurelien Larcher. All rights reserved.
#
include ../../../make-rules/shared-macros.mk

COMPONENT_NAME=         harfbuzz
COMPONENT_VERSION=      1.7.4
COMPONENT_FMRI=         library/c++/harfbuzz
COMPONENT_SUMMARY=      HarfBuzz - an OpenType text shaping engine. 
COMPONENT_CLASSIFICATION= System/Libraries
COMPONENT_SRC=          $(COMPONENT_NAME)-$(COMPONENT_VERSION)
COMPONENT_PROJECT_URL=  http://www.freedesktop.org/wiki/Software/HarfBuzz/
COMPONENT_ARCHIVE=      $(COMPONENT_SRC).tar.bz2
COMPONENT_ARCHIVE_HASH=	\
    sha256:b5d6ac8415f97f3540d73f3f91c41c5c10f8a4d76350f11a7184062aae88ac0b
COMPONENT_ARCHIVE_URL=	\
    http://www.freedesktop.org/software/harfbuzz/release/$(COMPONENT_ARCHIVE)
COMPONENT_LICENSE=      MIT

include $(WS_MAKE_RULES)/prep.mk
include $(WS_MAKE_RULES)/configure.mk
include $(WS_MAKE_RULES)/ips.mk

PATH=$(PATH.gnu)

CONFIGURE_OPTIONS+=	--enable-shared
CONFIGURE_OPTIONS+=	--disable-static
CONFIGURE_OPTIONS+=	--with-graphite2=yes
CONFIGURE_OPTIONS+=	--with-freetype=yes

LDFLAGS += -lm

unexport SHELLOPTS

COMPONENT_TEST_MASTER = $(COMPONENT_TEST_RESULTS_DIR)/results-all.master

COMPONENT_TEST_TRANSFORMS += \
        '-n ' \
        '-e "/TOTAL:/p" ' \
        '-e "/SKIP:/p" ' \
        '-e "/PASS:/p" ' \
        '-e "/FAIL:/p" ' \
        '-e "/ERROR:/p" '

build: $(BUILD_32_and_64)

install: $(INSTALL_32_and_64)

test: $(TEST_32_and_64)

REQUIRED_PACKAGES += library/c++/graphite2
REQUIRED_PACKAGES += library/desktop/cairo
REQUIRED_PACKAGES += library/glib2
REQUIRED_PACKAGES += library/icu
REQUIRED_PACKAGES += system/library
REQUIRED_PACKAGES += system/library/freetype-2
REQUIRED_PACKAGES += system/library/g++-4-runtime
REQUIRED_PACKAGES += system/library/math
