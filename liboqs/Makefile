# SPDX-License-Identifier: GPL-2.0-only

include $(TOPDIR)/rules.mk

PKG_NAME:=liboqs
PKG_SOURCE_DATE:=2024-10-26
PKG_SOURCE_VERSION:=6f30d7ef49ca590979d7a085cd662f00bb6855fe
PKG_RELEASE:=2
PKG_BUILD_FLAGS:=no-mips16 gc-sections

PKG_BUILD_PARALLEL:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL=https://github.com/open-quantum-safe/liboqs.git
PKG_MIRROR_HASH:=e0a9f4f20549bfece3d625c81259bf5f7fe9a12581463335d625526f4b02280a

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

#
# OPENSSL_ROOT_DIR
# OQS_USE_OPENSSL=on

CMAKE_OPTIONS += \
 -DBUILD_SHARED_LIBS=ON  \
 -DOQS_USE_OPENSSL=ON  \
 -DOQS_MINIMAL_BUILD="KEM_kyber_768;KEM_ml_kem_768;"

#cmake -DOQS_MINIMAL_BUILD="KEM_kyber_768;KEM_alg_ml_kem_76;SIG_dilithium_3"
#
# x25519_mlkem768:x25519_kyber768:p384_kyber768:x25519:secp384r1:x448:secp256r1:secp521r1;
#

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
