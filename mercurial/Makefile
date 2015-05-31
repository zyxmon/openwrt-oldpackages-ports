#
# Copyright (C) 2006-2011 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=mercurial
PKG_VERSION:=3.3.3
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=http://mercurial.selenic.com/release
PKG_MD5SUM:=8648a6980fc12a5a424abe809ab4c6e5

include $(INCLUDE_DIR)/package.mk
$(call include_mk, python-package.mk)

define Package/mercurial
  SECTION:=net
  CATEGORY:=Network
  DEPENDS:=+python
  TITLE:=Mercurial Source Control Management (SCM) system
  URL:=http://mercurial.selenic.com/
  SUBMENU:=Version Control Systems
endef

define Package/mercurial/description
  A fast, lightweight Source Control Management system designed for efficient
  handling of very large distributed projects.
endef

define Build/Compile
	$(call Build/Compile/PyMod,, \
		install --prefix="$(PKG_INSTALL_DIR)", \
    )
endef

define Package/mercurial/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) $(PKG_INSTALL_DIR)/bin $(1)/opt/
	$(CP) $(PKG_INSTALL_DIR)/lib $(1)/opt/
	$(SED) 's!/usr/bin/env python!/Apps/opt/bin/python!' $(1)/opt/bin/hg
endef

$(eval $(call BuildPackage,mercurial))
