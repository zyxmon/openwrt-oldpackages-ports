#
# Copyright (C) 2006-2009 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
# Used by rrdtool only, no reason to update.

include $(TOPDIR)/rules.mk

PKG_NAME:=cgilib
PKG_VERSION:=0.7
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=http://www.infodrom.org/projects/cgilib/download
PKG_MD5SUM:=2c7053f58dfb06f7a80a112797ed7e86

PKG_FIXUP:=autoreconf
PKG_BUILD_DEPENDS:=libltdl

LIBTOOL="$(STAGING_DIR)/host/bin/libtool"

include $(INCLUDE_DIR)/package.mk

define Package/cgilib
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=Simple CGI Library
  URL:=http://www.infodrom.org/projects/cgilib/
endef

TARGET_CFLAGS += $(FPIC)

define Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR) \
		$(TARGET_CONFIGURE_OPTS) \
                OFLAGS="$(TARGET_CFLAGS)" \
		DESTDIR="$(PKG_INSTALL_DIR)" \
		LIBTOOL="$(LIBTOOL)" \
                install
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/opt/include
	$(CP) $(PKG_INSTALL_DIR)/Apps/opt/include/cgi.h $(1)/opt/include/
	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) $(PKG_INSTALL_DIR)/Apps/opt/lib/libcgi.{a,so*} $(1)/opt/lib/
endef

define Package/cgilib/install
	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) $(PKG_INSTALL_DIR)/Apps/opt/lib/libcgi.so.* $(1)/opt/lib/
endef

$(eval $(call BuildPackage,cgilib))
