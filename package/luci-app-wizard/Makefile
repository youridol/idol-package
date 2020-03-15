#
# Copyright (C) 2017-2019 Chen Minqiang <ptpt52@gmail.com>
#
# This is free software, licensed under the GNU General Public License v3.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=luci-app-wizard
PKG_VERSION:=1.0.1
PKG_RELEASE:=1

PKG_LICENSE:=GPLv3
PKG_LICENSE_FILES:=LICENSE
PKG_MAINTAINER:=Chen Minqiang <ptpt52@gmail.com>

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)

include $(INCLUDE_DIR)/package.mk

define Package/luci-app-wizard
	CATEGORY:=Youridol
	TITLE:=LuCI Support for wizard
	PKGARCH:=all
	DEPENDS:=
endef

define Package/luci-app-wizard/description
	LuCI Support for wizard.
endef

define Build/Prepare

endef

define Build/Configure
endef

define Build/Compile
endef

define Package/luci-app-wizard/conffiles
/etc/config/wizard
endef

define Package/luci-app-wizard/postinst
#!/bin/sh
if [ -z "$$IPKG_INSTROOT" ]; then
  ( . /etc/uci-defaults/40_luci-app-wizard )
  rm -f /etc/uci-defaults/40_luci-app-wizard
  ( . /etc/uci-defaults/96-wizard-defaults )
  rm -f /etc/uci-defaults/96-wizard-defaults

  rm -rf /tmp/luci-indexcache /tmp/luci-modulecache
fi

exit 0
endef

define Package/luci-app-wizard/install
	$(INSTALL_DIR) $(1)/usr/lib/lua/luci/controller
	$(INSTALL_DATA) ./luasrc/controller/*.lua $(1)/usr/lib/lua/luci/controller/
	$(INSTALL_DIR) $(1)/usr/lib/lua/luci/model/cbi/wizard
	$(INSTALL_DATA) ./luasrc/model/cbi/wizard/*.lua $(1)/usr/lib/lua/luci/model/cbi/wizard/
	$(INSTALL_DIR) $(1)/etc/config
	$(INSTALL_DATA) ./root/etc/config/wizard $(1)/etc/config/wizard
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./root/etc/init.d/wizard $(1)/etc/init.d/wizard
	$(INSTALL_DIR) $(1)/etc/uci-defaults
	$(INSTALL_DATA) ./root/etc/uci-defaults/40_luci-app-wizard $(1)/etc/uci-defaults/40_luci-app-wizard
	$(INSTALL_DATA) ./uci.defaults $(1)/etc/uci-defaults/96-wizard-defaults
	$(INSTALL_DIR) $(1)/usr/lib/lua/luci/i18n
	po2lmo ./po/zh-cn/wizard.po $(1)/usr/lib/lua/luci/i18n/wizard.po.zh-cn.lmo

endef

$(eval $(call BuildPackage,luci-app-wizard))
