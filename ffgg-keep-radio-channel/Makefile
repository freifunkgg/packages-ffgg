include $(TOPDIR)/rules.mk

PKG_NAME:=ffgg-keep-radio-channel
PKG_VERSION:=2

PKG_BUILD_DIR := $(BUILD_DIR)/$(PKG_NAME)

include $(TOPDIR)/../package/gluon.mk

define Package/$(PKG_NAME)
  SECTION:=ffgg
  CATEGORY:=Customization
  MAINTAINER:=Freifunk Groß-Gerau
  TITLE:=Keep Radio Channel after update
  DEPENDS:=+gluon-core
endef

define Package/gluon-legacy/description
	Keep Radio Channel after update script
endef

define Build/Prepare
	mkdir -p $(PKG_BUILD_DIR)
endef

define Build/Compile
	$(call GluonSrcDiet,./luasrc,$(PKG_BUILD_DIR)/luadest/)
endef

define Package/$(PKG_NAME)/install
	$(CP) $(PKG_BUILD_DIR)/luadest/* $(1)/
endef

define Package/$(PKG_NAME)/postinst
#!/bin/sh
$(call GluonCheckSite,check_site.lua)
endef

$(eval $(call BuildPackage,$(PKG_NAME)))

