#
# Copyright (C) 2010-2011 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=ibrdtnd
PKG_VERSION:=0.12.1
PKG_RELEASE=0.1

#PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
#PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_URL:=https://github.com/thuydang/ibrdtn.git
PKG_SOURCE_PROTO:=git

PKG_MAINTAINER:=Thuy Dang <thuydang@github>

PKG_FIXUP:=autoreconf
PKG_BUILD_DIR := $(BUILD_DIR)/$(PKG_NAME)

include $(INCLUDE_DIR)/package.mk
#include $(INCLUDE_DIR)/cmake.mk

define Package/ibrdtnd/Default
  DEPENDS:=ibrcommon
	URL:=http://blah.com
endef

define Package/ibrdtnd/Default
	ibrdtn daemon	
endef

define Package/ibrcommon
  SECTION:=net
  CATEGORY:=Network
  SUBMENU:=Routing
  TITLE:=ibrdtn common
	URL:=http://trac.ibr.cs.tu-bs.de/project-cm-2012-ibrdtn/wiki/source/
endef
  #DEPENDS:=+libubox

define Package/ibrcommon/description
	Common lib reqired for ibrdtn	
endef

define Package/ibrdtnd
  SECTION:=net
  CATEGORY:=Network
  SUBMENU:=Routing
  TITLE:=ibrdtn daemon and tools
	URL:=http://trac.ibr.cs.tu-bs.de/project-cm-2012-ibrdtn/wiki/source/
  DEPENDS:=+ibrcommon
endef

define Package/ibrdtnd/description
	$(call Package/ibrdtnd/Default/description)
	This package depends on ibrcommon
endef

CONFOPTS += \
	--with-openssl \
	--with-curl

#define Build/Configure
#  $(call Build/Configure/Default,--with-linux-headers=$(LINUX_DIR))
#endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include
	$(CP) $(PKG_INSTALL_DIR)/usr/include/* $(1)/usr/include/
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libibr*.so* $(1)/usr/lib/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libibr*.*a $(1)/usr/lib/
	$(INSTALL_DIR) $(1)/usr/lib/pkgconfig
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/lib/pkgconfig/*.pc \
		$(1)/usr/lib/pkgconfig/
endef

#TARGET_CFLAGS += -I$(STAGING_DIR)/usr/include

define Package/ibrdtnd/install
	$(INSTALL_DIR) $(1)/etc/config
	$(INSTALL_CONF) $(PKG_INSTALL_DIR)/etc/config/ibrdtnd.conf $(1)/etc/config/ibrdtnd.conf
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/* $(1)/usr/bin/
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/sbin/dtnd $(1)/usr/sbin/dtnd
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/sbin/dtntunnel $(1)/usr/sbin/dtntunnel
endef

$(eval $(call BuildPackage,ibrdtnd))
$(eval $(call BuildPackage,ibrcommon))
