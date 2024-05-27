# SPDX-License-Identifer: GPL-3.0-only
#
# Copyright (C) 2020 - ntop.org and contributors
# Copyright (C) 2021-2022 ImmortalWrt.org

include $(TOPDIR)/rules.mk

PKG_NAME:=n2n
PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/ntop/n2n.git
PKG_SOURCE_VERSION:=d8b02bcbdb7ee8aa33244b3f6fabd8dfc547571a
PKG_SOURCE_DATE:=20231024
PKG_MIRROR_HASH:=skip
PKG_VERSION:=3.0.0-$(PKG_SOURCE_DATE)-$(call version_abbrev,$(PKG_SOURCE_VERSION))
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz

PKG_LICENSE:=GPL-3.0
PKG_LICENSE_FILE:=LICENSE
PKG_MAINTAINER:=Emanuele Faranda <faranda@ntop.org>

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/n2n/template
  SECTION:=net
  CATEGORY:=Network
  SUBMENU:=VPN
  TITLE:=N2N Peer-to-peer VPN (v3.0-stable)
  URL:=http://www.ntop.org/n2n
  DEPENDS:=+libopenssl +libpthread +libzstd
endef

define Package/n2n
  $(call Package/n2n/template)
  DEPENDS+=+libcap +kmod-tun +resolveip
endef

define Package/n2n/description
  This package contains client node and supernode for the N2N infrastructure.
endef

define Package/n2n/conffiles
/etc/config/n2n
endef

define Package/n2n-utils
  $(call Package/n2n/template)
  DEPENDS+=+n2n +libpcap
endef

define Package/n2n-utils/description
  This package contains extend utilities for the N2N infrastructure.
endef

CMAKE_OPTIONS+= \
	-DCMAKE_BUILD_TYPE=Release \
	-DN2N_OPTION_USE_PTHREAD=ON \
	-DN2N_OPTION_USE_OPENSSL=ON \
	-DN2N_OPTION_USE_PCAPLIB=ON \
	-DN2N_OPTION_USE_ZSTD=ON

define Package/n2n/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/sbin/edge $(1)/usr/bin/n2n-edge
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/sbin/supernode $(1)/usr/bin/n2n-supernode

	$(INSTALL_DIR) $(1)/etc/config
	$(INSTALL_CONF) ./files/n2n.config $(1)/etc/config/n2n
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/n2n.init $(1)/etc/init.d/n2n
	$(INSTALL_DIR) $(1)/etc/uci-defaults
	$(INSTALL_BIN) ./files/n2n-migrate-conf.sh $(1)/etc/uci-defaults/50-n2n-migrate-conf
endef

define Package/n2n-utils/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/n2n-benchmark $(1)/usr/bin/
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/n2n-decode $(1)/usr/bin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/n2n-keygen $(1)/usr/bin/
endef

$(eval $(call BuildPackage,n2n))
$(eval $(call BuildPackage,n2n-utils))
