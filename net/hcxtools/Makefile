#
# Copyright (C) 2019 Andreas Nilsen <adde88@gmail.com>
# Copyright (C) 2024 Xiaok <xiaok@openwrt.org>
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=hcxtools
PKG_VERSION:=6.2.7
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://codeload.github.com/zerbea/hcxtools/tar.gz/$(PKG_VERSION)?
PKG_HASH:=c9d69b5ddcf61c3deff687fad6c17197970cc75c5dbc7706b31c138bf0c784e1

PKG_MAINTAINER:=Andreas Nilsen <adde88@gmail.com>
PKG_LICENSE:=MIT
PKG_LICENSE_FILES:=license.txt

include $(INCLUDE_DIR)/package.mk

define Package/hcxtools
  SECTION:=net
  CATEGORY:=Network
  DEPENDS:=+libpthread +libpcap +zlib +libcurl +libopenssl
  TITLE:=hcxtools
  URL:=https://github.com/ZerBea/hcxtools
  SUBMENU:=Wireless
endef

define Package/hcxtools/description
  Set of tools convert packets from captures (h = hash, c = capture, convert and calculate candidates, x = different hashtypes)
  for the use with latest hashcat or John the Ripper.
endef

define Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR)/ \
		$(TARGET_CONFIGURE_OPTS) \
		CFLAGS="$(TARGET_CFLAGS)"
endef

define Package/hcxtools/install
	$(INSTALL_DIR) $(1)/sbin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/hcxeiutool	$(1)/sbin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/hcxessidtool	$(1)/sbin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/hcxhash2cap	$(1)/sbin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/hcxhashcattool	$(1)/sbin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/hcxhashtool	$(1)/sbin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/hcxmactool	$(1)/sbin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/hcxpcapngtool	$(1)/sbin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/hcxpmkidtool	$(1)/sbin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/hcxpmktool	$(1)/sbin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/hcxpsktool	$(1)/sbin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/hcxwltool	$(1)/sbin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/whoismac	$(1)/sbin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/wlancap2wpasec	$(1)/sbin/
endef

$(eval $(call BuildPackage,hcxtools))
