#
# Copyright (C) 2006-2010 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=mutt
PKG_VERSION:=1.5.23
PKG_RELEASE:=1

PKG_SOURCE_URL:=https://bitbucket.org/mutt/mutt/downloads \
	ftp://ftp.mutt.org/mutt
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_MD5SUM:=11f5b6a3eeba1afa1257fe93c9f26bff

PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/mutt
  SECTION:=mail
  CATEGORY:=Mail
  DEPENDS:=+libopenssl +libncursesw +libidn
  TITLE:=Console mail client
  URL:=http://www.mutt.org/
endef

define Package/mutt/description
	Mutt is a small but very powerful text-based mail client for Unix
	operating systems.
endef

CONFIGURE_ARGS += \
	--includedir=$(PKG_BUILD_DIR)/. \
	--oldincludedir=$(PKG_BUILD_DIR)/. \
	--disable-pgp \
	--enable-pop \
	--enable-imap \
	--enable-smtp \
	--with-ssl \
	--with-idn

define Package/mutt/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/Apps/opt/bin/mutt $(1)/opt/bin/
endef

$(eval $(call BuildPackage,mutt))
