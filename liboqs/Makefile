# SPDX-License-Identifier: GPL-2.0-only

include $(TOPDIR)/rules.mk

PKG_NAME:=liboqs
PKG_SOURCE_DATE:=2024-06-04
PKG_SOURCE_VERSION:=5dd87dcaafa6f90e983ef464f9f6a75f9485fb26
PKG_RELEASE:=1
PKG_BUILD_FLAGS:=no-mips16 gc-sections

PKG_BUILD_PARALLEL:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL=https://github.com/open-quantum-safe/liboqs.git
PKG_MIRROR_HASH:=840f298693717bf69dd045a8ec3787db6a9d06bd52259fdd138a6b768840c7f2

PKG_MAINTAINER:=Matt Noble <matt@mattnoble.com>
PKG_LICENSE:=GPL-2.0-only

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/liboqs
  SECTION:=libs
  CATEGORY:=Libraries
  DEPENDS:=+libopenssl
  TITLE:= liboqs, a collection of open source implementations of quantum-safe key encapsulation mechanism
endef

ifdef CONFIG_aarch64
    #CONFIGURE_ARGS += --enable-armasm
    TARGET_CFLAGS:=$(TARGET_CFLAGS:-mcpu%=-mcpu%+crypto)
endif

CMAKE_OPTIONS += \
 -DBUILD_SHARED_LIBS=ON

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include/oqs
	$(CP) $(PKG_INSTALL_DIR)/usr/include/* $(1)/usr/include/
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/* $(1)/usr/lib/
endef

define Package/liboqs/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/*.so* $(1)/usr/lib
endef

$(eval $(call BuildPackage,liboqs))
