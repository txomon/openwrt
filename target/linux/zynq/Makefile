#
# Copyright (C) 2007-2014 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

ARCH:=arm
BOARD:=zynq
BOARDNAME:=Xilinx Zynq7000 silicons
FEATURES:=usb gpio arm_v7
CPU_TYPE:=cortex-a9
SUBTARGETS:=zedboard

LINUX_VERSION:=3.13.7

MAINTAINER:=Javier Domingo Cansino <javierdo1@gmail.com>

include $(INCLUDE_DIR)/target.mk

define Target/Description
	Build firmware images for Zynq based boards
endef

$(eval $(call BuildTarget))
