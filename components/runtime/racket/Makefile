#
# CDDL HEADER START
#
# The contents of this file are subject to the terms of the
# Common Development and Distribution License (the "License").
# You may not use this file except in compliance with the License.
#
# You can obtain a copy of the license at usr/src/OPENSOLARIS.LICENSE
# or http://www.opensolaris.org/os/licensing.
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

# Copyright 2019, Richard Lowe.

include ../../../make-rules/shared-macros.mk

COMPONENT_NAME=         racket
COMPONENT_VERSION=      7.3
COMPONENT_SUMMARY=      Racket language
COMPONENT_PROJECT_URL=  http://www.racket-lang.org
COMPONENT_FMRI=         runtime/racket
COMPONENT_CLASSIFICATION=Development/Other Languages
COMPONENT_SRC=          $(COMPONENT_NAME)-$(COMPONENT_VERSION)
# Pure src, takes _forever_ to build
#COMPONENT_ARCHIVE=	$(COMPONENT_NAME)-$(COMPONENT_VERSION)-src.tgz
#COMPONENT_ARCHIVE_HASH= \
#  sha256:d49b11de4aa8f62d23d096134d4246f6cbd7a1da326645fecc072d28ad38c040
# src with packages pre-byte compiled
COMPONENT_ARCHIVE=      $(COMPONENT_NAME)-$(COMPONENT_VERSION)-src-builtpkgs.tgz
COMPONENT_ARCHIVE_HASH= \
  sha256:6324ab7212ca2ba89cf6c5cee743adb0e9bc0b3dd9d1ec30abb55134ff06a601
COMPONENT_ARCHIVE_URL=	https://mirror.racket-lang.org/installers/$(COMPONENT_VERSION)/$(COMPONENT_ARCHIVE)
COMPONENT_LICENSE=      LGPLv3,GPLv3,libscheme

include $(WS_MAKE_RULES)/prep.mk
include $(WS_MAKE_RULES)/configure.mk
include $(WS_MAKE_RULES)/ips.mk

CONFIGURE_SCRIPT = $(SOURCE_DIR)/src/configure
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

COMPONENT_BUILD_ARGS += $(JOBS:%=-j%)

build:		$(BUILD_32)

install:	$(INSTALL_32)

test:		$(TEST_32)

# Auto-generated dependencies
REQUIRED_PACKAGES += library/libffi
REQUIRED_PACKAGES += SUNWcs
REQUIRED_PACKAGES += system/library
REQUIRED_PACKAGES += system/library/math
