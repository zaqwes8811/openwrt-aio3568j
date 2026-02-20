#
# Copyright (C) 2025 Your Name/Organization
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=bcmdhd-dkms
PKG_VERSION:=101.10.591.52.27-6
PKG_RELEASE:=1

# Since we are using locally copied source, no PKG_SOURCE_URL is needed.
PKG_LICENSE:=Proprietary
PKG_LICENSE_FILES:=

PKG_SOURCE:=$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://github.com/armbian/bcmdhd-dkms/archive/refs/tags/
PKG_HASH:=ac4719559a2e0dad7071b81df5f174211c3618b6e3eb4cc5a8f4174edbb621ed

PKG_EXTMOD_SUBDIRS=src


include $(INCLUDE_DIR)/kernel.mk
include $(INCLUDE_DIR)/package.mk

define KernelPackage/bcmdhd
  SUBMENU:=Wireless Drivers
  TITLE:=Broadcom BCMDHD SDIO WiFi driver
  DEPENDS:=+kmod-mmc +@DRIVER_11N_SUPPORT @PCI_SUPPORT +kmod-cfg80211 +kmod-mac80211
  FILES:=$(PKG_BUILD_DIR)/src/dhd_static_buf_sdio.ko
  AUTOLOAD:=$(call AutoLoad,50,bcmdhd)
  MENU:=1
endef

define KernelPackage/bcmdhd/description
  Kernel module for Broadcom BCMDHD based WiFi chips (e.g., AP6275S).
endef

define Build/Compile
	+$(KERNEL_MAKE) $(PKG_JOBS) \
		$(PKG_MAKE_FLAGS) \
		M="$(PKG_BUILD_DIR)/src" \
		modules \
		CONFIG_BCMDHD=y CONFIG_BCMDHD_SDIO=y \
		CONFIG_CFG80211=y CONFIG_AP6XXX=y
endef

$(eval $(call KernelPackage,bcmdhd))