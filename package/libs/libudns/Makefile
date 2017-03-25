#
# Copyright (C) 2012 ezbox project
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=udns
PKG_VERSION:=0.4
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=http://www.corpit.ru/mjt/udns
PKG_HASH:=115108dc791a2f9e99e150012bcb459d9095da2dd7d80699b584ac0ac3768710

include $(INCLUDE_DIR)/package.mk

define Package/libudns
  SECTION:=net
  CATEGORY:=Network
  URL:=http://www.corpit.ru/mjt/udns.html
  SUBMENU:=IP Addresses and Names
  TITLE:=udns library, stub DNS resolver -  shared libraries 
endef

define Package/libudns/description
The DNS library, udns, implements thread-safe stub DNS resolver functionality, which may be used both traditional, syncronous way and asyncronously, with application-supplied event loop.
endef

export BUILD_CC="$(TARGET_CC)"
export CC="$(TARGET_CC)"
export AR="$(TARGET_CROSS)ar"
export RANLIB="$(TARGET_CROSS)ranlib"

define Build/Configure
	(cd $(PKG_BUILD_DIR); \
		./configure \
		--enable-cross_compile \
		$(DISABLE_IPV6) \
	)
endef

define Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR) all
	$(MAKE) -C $(PKG_BUILD_DIR) shared
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include/udns
	$(CP) $(PKG_BUILD_DIR)/udns.h $(1)/usr/include/udns
	$(CP) $(PKG_BUILD_DIR)/udns.h $(1)/usr/include

	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_BUILD_DIR)/lib*.{a,so*} $(1)/usr/lib
endef

define Package/libudns/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_BUILD_DIR)/lib*.so* $(1)/usr/lib
endef

$(eval $(call BuildPackage,libudns))
