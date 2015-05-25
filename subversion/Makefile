#
# Copyright (C) 2007-2011 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=subversion
PKG_VERSION:=1.6.23
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_SOURCE_URL:=http://subversion.tigris.org/downloads
PKG_MD5SUM:=5d621281ce9d3448e1437cb006331f57

PKG_FIXUP:=autoreconf
PKG_MACRO_PATHS:=build/ac-macros

include $(INCLUDE_DIR)/package.mk

define Package/subversion/Default
  SECTION:=net
  CATEGORY:=Network
  TITLE:=A compelling replacement for CVS
  DEPENDS:=+zlib +libneon +libaprutil
  URL:=http://subversion.apache.org/
  SUBMENU:=Version Control Systems
endef

define Package/subversion/Default/description
	Subversion is a free/open-source version control system. That is,
	Subversion manages files and directories, and the changes made to them,
	over time. This allows you to recover older versions of your data, or
	examine the history of how your data changed. In this regard, many
	people think of a version control system as a sort of time machine.
endef

define Package/subversion-libs
  $(call Package/subversion/Default)
  DEPENDS+=+unixodbc
  TITLE:=subversion libs
endef

define Package/subversion-libs/description
  $(call Package/subversion/Default/description)
  This package contains the subversion libraries.
endef

define Package/subversion-client
  $(call Package/subversion/Default)
  DEPENDS+=subversion-libs
  TITLE:=subversion client tools
endef

define Package/subversion-client/description
  $(call Package/subversion/Default/description)
  This package contains the subversion client tools.
endef

define Package/subversion-server
  $(call Package/subversion/Default)
  DEPENDS+=subversion-libs
  TITLE:=subversion server
endef

define Package/subversion-server/description
  $(call Package/subversion/Default/description)
  This package contains the subversion server.
endef

define Package/subversion-server/conffiles
/opt/etc/config/subversion
endef

TARGET_CFLAGS += $(FPIC)
TARGET_CPPFLAGS += -D_LARGEFILE64_SOURCE -D_FILE_OFFSET_BITS=64 -D_GNU_SOURCE

CONFIGURE_ARGS += \
	--with-apr="$(STAGING_DIR)/opt/bin/apr-1-config" \
	--with-apr-util="$(STAGING_DIR)/opt/bin/apu-1-config" \
	--with-neon="$(STAGING_DIR)/opt" \
	--disable-mod-activation \
	--without-ruby-sitedir \
	--without-swig \
	--with-jikes=no \
	--without-junit \
	--without-berkeley-db \
	--with-ssl \
	--disable-neon-version-check \
	--with-apxs=no \
	--without-sasl \

CONFIGURE_VARS += \
	svn_lib_neon=yes \
	LDFLAGS="$(TARGET_LDFLAGS) -lcrypt -lm \
		-lz -lpthread -L$(TOOLCHAIN_DIR)/opt/lib \
		-L$(TOOLCHAIN_DIR)/lib" \
	CPPFLAGS="$(TARGET_CPPFLAGS)" \

define Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR) \
		DESTDIR="$(PKG_INSTALL_DIR)" \
		all local-install
endef

define Package/subversion-libs/install
	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/libsvn_*.so.* $(1)/opt/lib/
endef

define Package/subversion-client/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/{svn,svnversion,svnsync} $(1)/opt/bin/
endef

define Package/subversion-server/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/svn{look,admin,dumpfilter,serve} $(1)/opt/bin/
endef

$(eval $(call BuildPackage,subversion-libs))
$(eval $(call BuildPackage,subversion-client))
$(eval $(call BuildPackage,subversion-server))