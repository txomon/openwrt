#
# Copyright (C) 2014 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=u-boot
PKG_VERSION:=2014.04
PKG_RELEASE:=0

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=git://github.com/xilinx/u-boot-xlnx
PKG_SOURCE_VERSION:=2a0536fa48db1fc5332e3cd33b846d0da0c8bc1e
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(BUILD_VARIANT)/$(PKG_NAME)-$(PKG_VERSION)

include $(INCLUDE_DIR)/package.mk

define uboot/Default
  TITLE:=
  CONFIG:=
  IMAGE:=
endef

define uboot/zedboard
  TITLE:=U-Boot for Zedboard Zynq
  CONFIG:=zynq_zc70x
endef

UBOOTS := \
	zedboard

define Package/uboot/template
define Package/uboot-zynq-$(1)
  SECTION:=boot
  CATEGORY:=Boot Loaders
  DEPENDS:=@TARGET_zynq
  TITLE:=$(2)
  URL:=http://www.wiki.xilinx.com/U-boot
  VARIANT:=$(1)
  MAINTAINER:=Javier Domingo Cansino <javierdo1@gmail.com
endef
endef

define BuildUBootPackage
	$(eval $(uboot/Default))
	$(eval $(uboot/$(1)))
	$(call Package/uboot/template,$(1),$(TITLE))
endef

ifdef BUILD_VARIANT
$(eval $(call uboot/$(BUILD_VARIANT)))
UBOOT_CONFIG:=$(if $(CONFIG),$(CONFIG),$(BUILD_VARIANT))
UBOOT_IMAGE:=$(if $(IMAGE),$(IMAGE),$(BUILD_VARIANT)-u-boot.img)
endif

define Build/Configure
	$(MAKE) -C $(PKG_BUILD_DIR) $(UBOOT_CONFIG)_config
endef

define Build/Compile
	$(MAKE) $(PKG_JOBS) -C $(PKG_BUILD_DIR) \
		CROSS_COMPILE=$(TARGET_CROSS)
endef


define Package/uboot/install/template
define Package/uboot-$(1)/install
	$(INSTALL_DIR) $$(1)
	$(CP) $(PKG_BUILD_DIR)/u-boot.bin $(BIN_DIR)/$(2)
endef
endef


$(foreach u,$(UBOOTS), \
	$(eval $(call Package/uboot/install/template,$(u),$(BOARD)-$(u)-u-boot.img)) \
)

$(foreach u,$(UBOOTS), \
	$(eval $(call BuildUBootPackage,$(u))) \
	$(eval $(call BuildPackage,uboot-$(u))) \
)
