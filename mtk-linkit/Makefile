# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.

include $(TOPDIR)/rules.mk

PKG_NAME:=mtk-linkit
PKG_RELEASE:=1

include $(INCLUDE_DIR)/package.mk

define Package/mtk-linkit
	TITLE:=LinkIt Smart board support package
	DEPENDS:=@TARGET_ramips_mt76x8_DEVICE_LinkIt7688 \
		+gdbserver +curl +strace +coreutils \
		+blockd \
		+git +git-http +samba36-server \
		+uboot-envtools \
		+kmod-fs-vfat +kmod-usb-storage \
		+kmod-nls-base +kmod-nls-cp437 +kmod-nls-iso8859-1 \
		+kmod-nls-iso8859-15 +kmod-nls-iso8859-2 +kmod-nls-utf8 \
		+@KERNEL_DEVMEM
		#+cgi-io +rpcd
		#+kmod-sdhci-mt7620 
		#+uhttpd 
		#+luci +luci-theme-openwrt +luci-app-samba +luci-lib-json
		#+avrdude +spi-tools +yunbridge
		#+luci-app-mjpg-streamer +kmod-i2c-core
		#+python +python-pyserial +python-pip +hidapi
		#+avahi-nodbus-daemon +mjpg-streamer
		#+tcpdump-mini
		#+kmod-video-core
		#+kmod-sound-core +madplay-alsa +alsa-utils
		#+mtk-linkit-webui
		#+kmod-sound-mt7620
		#+kmod-video-uvc
		#+kmod-fs-exfat
		#+rpcd-mod-rpcsys
		#+node +node-hid +node-cylon-firmata
		#+rpcd-mod-iwinfo
		#+coreutils-stty
		#+libmraa +libupm 
		#+kmod-sound-mtk
		#+mtk-sdk-wifi
	DEFAULT:=y
endef

define Build/Prepare
	mkdir -p $(PKG_BUILD_DIR)
endef

define Build/Compile
        $(TARGET_CC) $(TARGET_CFLAGS) $(EXTRA_CFLAGS) -Wall -Werror -o $(PKG_BUILD_DIR)/pinmux src/pinmux.c ; \
        $(TARGET_CC) $(TARGET_CFLAGS) $(EXTRA_CFLAGS) -Wall -Werror -o $(PKG_BUILD_DIR)/refclk src/refclk.c
endef

define Package/mtk-linkit/install
	$(INSTALL_DIR) $(1)/sbin
	
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/pinmux $(1)/sbin/mt7688_pinmux
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/refclk $(1)/sbin/mt7688_reclk
	$(CP) ./files/* $(1)
endef

$(eval $(call BuildPackage,mtk-linkit))
