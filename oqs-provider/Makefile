# SPDX-License-Identifier: GPL-2.0-only

include $(TOPDIR)/rules.mk

PKG_NAME:=oqs-provider
PKG_SOURCE_DATE:=2024-10-08
PKG_SOURCE_VERSION:=7b6928e63d45cfb72487177748b63c7c8adc559d
PKG_RELEASE:=2

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL=https://github.com/open-quantum-safe/oqs-provider
PKG_MIRROR_HASH:=067f74863146558ed8b93bd077b694fe85805c92406233703d762636918c7e56

PKG_MAINTAINER:=David Bauer <mail@david-bauer.net>
PKG_LICENSE:=GPL-2.0-only

PKG_BUILD_DEPENDS:=liboqs

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/oqs-provider
  SECTION:=libs
  CATEGORY:=Libraries
  DEPENDS:=+libopenssl +liboqs
  TITLE:=Open Quantum Safe Provider of Openssl
endef

# We won't need unit tests
CMAKE_OPTIONS += -DWITH_UNIT_TESTS=0

# Make it explicit that we are cross-compiling
CMAKE_OPTIONS += -DCMAKE_CROSSCOMPILING=1

CMAKE_OPTIONS += \
 -DCMAKE_INSTALL_PREFIX=/usr \
 -DCMAKE_BUILD_TYPE:STRING=Release \
 -DOQS_KEM_ENCODERS=off \
 -Dliboqs_DIR=="$(STAGING_DIR)/usr/lib" 

define Package/oqs-provider/conffiles
  /etc/ssl/modules.cnf.d/oqs-provider.cnf
endef

#define Build/InstallDev
#	$(INSTALL_DIR) $(1)/usr/include/oss-modules
#	$(CP) $(PKG_INSTALL_DIR)/usr/include/* $(1)/usr/include/
#	$(INSTALL_DIR) $(1)/usr/lib
#	$(CP) $(PKG_INSTALL_DIR)/usr/lib/* $(1)/usr/lib/
#endef

define Package/oqs-provider/install
	$(INSTALL_DIR) $(1)/usr/lib/ossl-modules
	# I don't know why the this is getting installed to this path...
	$(CP) $(PKG_INSTALL_DIR)/$(STAGING_DIR)/usr/lib/* $(1)/usr/lib

	$(INSTALL_DIR) $(1)/etc/ssl/modules.cnf.d
#	$(INSTALL_DIR) $(1)/etc/ssl/modules.cnf.d $(1)/etc/config 
	$(CP) ./files/oqs-provider.cnf $(1)/etc/ssl/modules.cnf.d/

#	touch $(1)/etc/config/openssl
#	echo -e "\nconfig engine 'oqs-provider'\n\toption enabled '1'" >> $(1)/etc/config/openssl
endef

$(eval $(call BuildPackage,oqs-provider))
