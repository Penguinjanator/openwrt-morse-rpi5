#
# Copyright 2026 Build with Parallel
#
# Pi 5 counterpart of Morse's persistent-vars-storage-bcm2711.
# wizard-config depends on the virtual provide persistent-vars-storage;
# without this package it is silently dropped from bcm2712 images.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=persistent-vars-storage-bcm2712
PKG_RELEASE:=1

PKG_MAINTAINER:=Build with Parallel

include $(INCLUDE_DIR)/package.mk

define Package/persistent-vars-storage-bcm2712
  SECTION:=Utilities
  CATEGORY:=Morse Micro
  SUBMENU:=Hardware
  PROVIDES:=persistent-vars-storage
  TITLE:=Read key-value pairs from the Raspberry Pi 5 EEPROM
  DEPENDS:=+bcm27xx-utils @TARGET_bcm27xx_bcm2712
endef

define Package/persistent-vars-storage-bcm2712/description
  Satisfies wizard-config's persistent-vars-storage dependency on Pi 5.
  Reads Morse/OpenWrt keys from the BCM2712 bootloader EEPROM via vcgencmd,
  same interface as persistent-vars-storage-bcm2711 on Pi 4. Writes are not
  implemented (matching the Pi 4 package).
endef

define Build/Compile
endef

define Package/persistent-vars-storage-bcm2712/install
	$(INSTALL_DIR) $(1)/sbin
	$(INSTALL_BIN) ./files/sbin/persistent_vars_storage.sh $(1)/sbin/persistent_vars_storage.sh
endef

$(eval $(call BuildPackage,persistent-vars-storage-bcm2712))
