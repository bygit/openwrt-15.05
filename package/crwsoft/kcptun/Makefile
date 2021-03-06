#
# Copyright (C) 2015 OpenWrt-dist
# Copyright (C) 2016 Chen RuiWei <crwbak@gmail.com>
#
# This is free software, licensed under the GNU General Public License v3.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=kcptun
PKG_VERSION:=1.0
PKG_RELEASE=20160812

PKG_LICENSE:=GPLv3
PKG_LICENSE_FILES:=LICENSE
PKG_MAINTAINER:=Chen RuiWei <crwbak@gmail.com>

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)

include $(INCLUDE_DIR)/package.mk

define Package/kcptun
	SECTION:=net
	CATEGORY:=Extra packages
	TITLE:=a fast udp tunnel based on kcp protocol
	URL:=https://github.com/loveuall/kcptun
	DEPENDS:=+ipset +ip
	VARIANT:=
endef

define Build/Prepare
	$(CP) ./files/Makefile $(PKG_BUILD_DIR)/
endef

define Build/Configure
endef

define Build/Compile
endef

define Package/kcptun/install
	$(INSTALL_DIR) $(1)/usr/bin $(1)/etc/init.d $(1)/etc/uci-defaults $(1)/usr/share/kcptun $(1)/etc/config
ifeq ($(ARCH),arm)
	$(INSTALL_BIN) ./files/arm/kcpclient $(1)/usr/bin/
endif
ifeq ($(ARCH),aarch64)
	$(INSTALL_BIN) ./files/armv7/kcpclient $(1)/usr/bin/
endif
ifeq ($(ARCH),mips)
	# $(INSTALL_BIN) ./files/ar71xx/kcpclient $(1)/usr/bin/
endif
ifeq ($(ARCH),mipsel)
	# $(INSTALL_BIN) ./files/7620n/kcpclient $(1)/usr/bin/
endif
ifeq ($(ARCH),i386)
	$(INSTALL_BIN) ./files/x86/kcpclient $(1)/usr/bin/
endif
ifeq ($(ARCH),x86_64)
	$(INSTALL_BIN) ./files/x86_64/kcpclient $(1)/usr/bin/
endif
	$(INSTALL_BIN) ./files/kcptun.init $(1)/etc/init.d/kcptun
	$(INSTALL_DATA) ./files/kcptun.defaults $(1)/etc/uci-defaults/96-kcptun
	$(INSTALL_DATA) ./files/kcptun.firewall $(1)/usr/share/kcptun/firewall.include
	$(INSTALL_DATA) ./files/chnroute.txt $(1)/usr/share/kcptun/
	$(INSTALL_DATA) ./files/kcptun.config $(1)/etc/config/kcptun
endef

$(eval $(call BuildPackage,kcptun))
