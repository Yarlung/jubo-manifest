#
# Copyright (C) 2006-2011 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=fibers
PKG_VERSION:=v1.0.1
PKG_RELEASE:=2

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
#PKG_SOURCE_URL:=http://nodejs.org/dist/${PKG_VERSION}
#PKG_MD5SUM:=15849c6e10d7fad711d45590882edc52
#GIT_SOURCE:=https://github.com/brimstone/v8m-rb
#GIT_SOURCE:=/tmp/v8m-rb

#GYP_DEFINES:=v8_use_mips_abi_hardfloat=false v8_can_use_fpu_instructions=false
LIBS:=-I$(TOOLCHAIN_DIR)/i486-openwrt-linux-uclibc/include/c++/4.6.3/ \
	  -I$(TOOLCHAIN_DIR)/i486-openwrt-linux-uclibc/include/c++/4.6.3/i486-openwrt-linux-uclibc/\

include $(INCLUDE_DIR)/package.mk

define Package/fibers
  SECTION:=lang
  CATEGORY:=Languages
  TITLE:=fibers
endef

define Package/fibers/description
Node.js is a platform built on Chrome's JavaScript runtime for easily building fast, scalable network applications. Node.js uses an event-driven, non-blocking I/O model that makes it lightweight and efficient, perfect for data-intensive real-time applications that run across distributed devices.
endef

define Build/Prepare
	$(call Build/Prepare/Default)
endef

define Build/Configure
	(cd $(PKG_BUILD_DIR); \
	export LIBS="$(LIBS)"; \
	export CFLAGS="$(TARGET_CFLAGS) $(LIBS)"; \
	export CXXFLAGS="$(TARGET_CXXFLAGS) $(LIBS)"; \
    export GYPFLAGS="$(GYPFLAGS)"; \
	node-gyp -I$(TOOLCHAIN_DIR)/include --arch $(ARCH) configure; \
	);
endef

define Build/Compile
	(cd $(PKG_BUILD_DIR); \
	export CXX="$(TARGET_CXX)";\
	export CC="$(TARGET_CC)";\
	node-gyp build; \
	);
endef

define Package/fibers/install
	mkdir -p $(1)/usr/bin
endef

$(eval $(call BuildPackage,fibers))
