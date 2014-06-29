#
# Copyright (C) 2014 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

# Build information
PKG_NAME:=u-boot
PKG_VERSION:=2014.04
PKG_RELEASE:=0

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=git://github.com/xilinx/u-boot-xlnx
PKG_SOURCE_VERSION:=2a0536fa48db1fc5332e3cd33b846d0da0c8bc1e
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(BUILD_VARIANT)/$(PKG_NAME)-$(PKG_VERSION)


# Boards
include $(INCLUDE_DIR)/package.mk

define Package/uboot-zynq-zedboard
  SECTION:=boot
  CATEGORY:=Boot Loaders
  DEPENDS:=@TARGET_zynq
  TITLE:=U-Boot for Zedboard Zynq
  CONFIG:=zynq_zc70x
  URL:=http://www.wiki.xilinx.com/U-boot
  VARIANT:=$(1)
  MAINTAINER:=Javier Domingo Cansino <javierdo1@gmail.com
endef

define Package/uboot-zynq-zedboard/config
	source "package/boot/uboot-xilinx/Config.in"
endef

define Build/Prepare
	$(call Build/Prepare/Default)

  ifneq ($(CONFIG_XILINX_ISE_PATH),)
	$(CP) \
	 $(CONFIG_XILINX_ISE_PATH)/EDK/sw/lib/hwplatform_templates/zed_hw_platform/ps7_init.{c,h} \
	 $(PKG_BUILD_DIR)/board/xilinx/zynq
  endif
endef

define Package/uboot-zynq-zedboard/install
	$(INSTALL_DIR) $(1)
	$(CP) $(PKG_BUILD_DIR)/u-boot.img $(BIN_DIR)/zedboard-u-boot.img

  ifneq ($(CONFIG_XILINX_ISE_PATH),)
	$(CP) $(PKG_BUILD_DIR)/boot.bin $(BIN_DIR)/zedboard-boot.bin
  endif
endef

define Build/Configure
	$(MAKE) -C $(PKG_BUILD_DIR) zynq_zed_config
endef

define Build/Compile
	$(MAKE) $(PKG_JOBS) -C $(PKG_BUILD_DIR) \
		CROSS_COMPILE=$(TARGET_CROSS)
endef

$(eval $(call BuildPackage,uboot-zynq-zedboard))
