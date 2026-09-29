#
# Copyright 2026 Build with Parallel
#
# Morse luci-app-morseapwizard calls uci.load('umdns') on first paint, but
# its rpcd ACL never grants umdns. First-boot LuCI then fails with
# "uci/get {config:umdns} ... Permission denied" and the wizard hangs.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=luci-acl-umdns
PKG_RELEASE:=1

PKG_MAINTAINER:=Build with Parallel

include $(INCLUDE_DIR)/package.mk

define Package/luci-acl-umdns
  SECTION:=utils
  CATEGORY:=Utilities
  TITLE:=Grant LuCI/rpcd access to umdns UCI
  DEPENDS:=+luci-base +umdns
endef

define Package/luci-acl-umdns/description
  Adds an rpcd ACL so the Morse first-boot wizard and unauthenticated
  LuCI session can read/write /etc/config/umdns. Morse's own wizard ACL
  omits this config, which leaves the wizard stuck on "Loading view…".
endef

define Build/Compile
endef

define Package/luci-acl-umdns/install
	$(INSTALL_DIR) $(1)/usr/share/rpcd/acl.d
	$(INSTALL_DATA) ./files/luci-acl-umdns.json $(1)/usr/share/rpcd/acl.d/luci-acl-umdns.json
endef

define Package/luci-acl-umdns/postinst
#!/bin/sh
[ -n "$${IPKG_INSTROOT}" ] || /etc/init.d/rpcd reload
endef

$(eval $(call BuildPackage,luci-acl-umdns))
