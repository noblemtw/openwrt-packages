include $(TOPDIR)/rules.mk

PKG_NAME:=sysinfo
PKG_VERSION:=20241007

include $(INCLUDE_DIR)/package.mk

define Package/sysinfo
	SECTION:=utils
	CATEGORY:=Utilities
	TITLE:=eko.one.pl Services
	PKGARCH:=all
endef

define Build/Compile
endef

define Package/sysinfo/install
	$(INSTALL_DIR) $(1)/sbin
	$(INSTALL_BIN) ./files/sbin/sysinfo.sh $(1)/sbin

	$(INSTALL_DIR) $(1)/etc/profile.d/
	$(CP) ./files/etc/* $(1)/etc
	#$(INSTALL_CONF) ./files/etc/profile.d/99-sysinfo.sh $(1)/etc/profile.d/
endef

$(eval $(call BuildPackage,sysinfo))


