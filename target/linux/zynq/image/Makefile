#
# Copyright (C) 2014 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
include $(TOPDIR)/rules.mk
include $(INCLUDE_DIR)/image.mk

define Image/BuildKernel/Initramfs
	(cd $(TARGET_DIR); find . | cpio -o -H newc | gzip -9 >$(KDIR)/zedboard-rootfs.cpio.gz )
	mkimage -A arm -T ramdisk -C none -d $(KDIR)/zedboard-rootfs.cpio.gz $(BIN_DIR)/zedboard-uramdisk.image.gz
endef

define Image/BuildKernel
	mkimage -A arm -O linux -T kernel -C none -a 0x80000000 -e \
		0x80000000 \
		-n 'ARM OpenWrt Linux-$(LINUX_VERSION)' \
		-d $(KDIR)/vmlinux $(BIN_DIR)/zedboard-uImage
endef

define Image/Prepare
	$(LINUX_DIR)/scripts/dtc/dtc -O dtb $(LINUX_DIR)/arch/arm/boot/dts/zynq-zed.dts > $(BIN_DIR)/zedboard.dtb
endef

$(eval $(call BuildImage))
