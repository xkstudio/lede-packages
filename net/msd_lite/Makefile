#
# Copyright (C) 2006-2023 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=msd_lite
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_DATE:=2024-04-26
PKG_SOURCE_URL:=https://github.com/rozhuk-im/msd_lite.git
PKG_SOURCE_VERSION:=0143aaa812ef762d98269fbc9eeae56e7e60a4b2
PKG_MIRROR_HASH:=skip

PKG_LICENSE:=BSD-2-Clause
PKG_LICENSE_FILES:=LICENSE

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/msd_lite
  SECTION:=net
  CATEGORY:=Network
  TITLE:=Multi Stream daemon Lite
  URL:=https://github.com/rozhuk-im/msd_lite
  DEPENDS:= +libpthread
endef

define Package/msd_lite/description
Program for IP TV streaming on the network via HTTP
endef

define Package/msd_lite/conffiles
/etc/msd_lite/msd_lite.conf
endef

CMAKE_OPTIONS += \
	-DCONFDIR=/etc/msd_lite

define Package/msd_lite/install
	$(INSTALL_DIR) $(1)/etc/msd_lite $(1)/usr/bin
	$(INSTALL_CONF) $(PKG_BUILD_DIR)/conf/msd_lite.conf $(1)/etc/msd_lite/
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/msd_lite $(1)/usr/bin/
endef

$(eval $(call BuildPackage,msd_lite))
