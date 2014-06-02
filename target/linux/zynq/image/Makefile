#
# Copyright (C) 2014 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
include $(TOPDIR)/rules.mk
include $(INCLUDE_DIR)/image.mk

define Image/BuildKernel
	# Don't know if zedboard supports this, taken from amazon/image/Makefile...
	$(STAGING_DIR_HOST)/bin/lzma e $(KDIR)/vmlinux $(KDIR)/vmlinux.lzma
	mkimage -A arm -O linux -T kernel -C lzma -a 0x80000000 -e \
		0x80000000 \
		-n 'ARM OpenWrt Linux-$(LINUX_VERSION)' \
		-d $(KDIR)/vmlinux.lzma $(KDIR)/uImage
	cp $(KDIR)/uImage $(BIN_DIR)/zedboard-uImage
endef

define Image/Prepare
	$(LINUX_DIR)/scripts/dtc/dtc -O dtb $(LINUX_DIR)/arch/arm/boot/dts/zynq-zed.dts > $(BIN_DIR)/zedboard.dtb
endef

$(eval $(call BuildImage))
