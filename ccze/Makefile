#
# Copyright (C) 2011-2015 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=ccze
PKG_VERSION:=0.2.1
PKG_RELEASE:=2

PKG_SOURCE:=$(PKG_NAME)_$(PKG_VERSION).orig.tar.gz
PKG_SOURCE_URL:=http://ftp.debian.org/debian/pool/main/c/ccze/
PKG_HASH:=8263a11183fd356a033b6572958d5a6bb56bfd2dba801ed0bff276cfae528aa3


PKG_MAINTAINER:= 
PKG_LICENSE:=GPL-2.0-only
PKG_LICENSE_FILES:=COPYING

PKG_FIXUP:=autoreconf
PKG_INSTALL:=1
PKG_BUILD_PARALLEL:=1
PKG_BUILD_DEPENDS:=!USE_GLIBC:argp-standalone

include $(INCLUDE_DIR)/package.mk

define Package/ccze
  SECTION:=utils
  CATEGORY:=Utilities
  TITLE:=Fast C log colorizer
  URL:=http://ftp.debian.org/debian/pool/main/c/ccze/
  DEPENDS:= +libpcre +libncurses
  PKGARCH:=all
endef

define Package/ccze/description
This is CCZE, a fast log colorizer written in C, intended to be a
drop-in replacement for colorize (http://colorize.raszi.hu).
endef


ifndef CONFIG_USE_GLIBC
        CONFIGURE_VARS += LIBS="-largp"
endif

# Strip options that configure script does not recognize
CONFIGURE_ARGS:=$(filter-out    \
                  --disable-dependency-tracking \
                  --disable-nls \
                , $(CONFIGURE_ARGS))


#$(STAGING_DIR)/usr/lib/libargp.a
TARGET_LDFLAGS += \
        #$(if $(CONFIG_USE_GLIBC),,-largp) \
        (STAGING_DIR)/usr/lib/libargp.a \
        -Wl,--as-needed

define Package/ccze/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_DIR) $(1)/usr/lib/ccze
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/ccze $(1)/usr/bin/ccze
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/ccze/*.so* \
            $(1)/usr/lib/ccze
endef

$(eval $(call BuildPackage,ccze))
