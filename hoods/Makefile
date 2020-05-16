include $(TOPDIR)/rules.mk

PKG_NAME:=ffgg-hoods
PKG_VERSION:=1
PKG_RELEASE:=1

PKG_BUILD_DEPENDS := lua-cjson/host

PKG_BUILD_DIR := $(BUILD_DIR)/$(PKG_NAME)

include $(TOPDIR)/../package/gluon.mk

define Package/$(PKG_NAME)
  SECTION:=network
  CATEGORY:=Freifunk Nordwest
  TITLE:=Hoodjson file
endef

define Package/$(PKG_NAME)/description
	Hoodjson file
endef

define Build/Prepare
	mkdir -p $(PKG_BUILD_DIR)
endef

define Build/Configure
endef

define Build/Compile
	$(call GluonSrcDiet,./luasrc,$(PKG_BUILD_DIR)/luadest/)
endef

define Package/$(PKG_NAME)/install
	$(INSTALL_DIR) $(1)/lib/ffgg/hoods
	lua -e 'local cjson = require("cjson"); print(cjson.encode(cjson.decode(assert(io.open("./files/lib/ffgg/hoods/hoods.json"):read("*a")))))' > $(1)/lib/ffgg/hoods/hoods.json
	$(CP) $(PKG_BUILD_DIR)/luadest/* $(1)/
endef

$(eval $(call BuildPackage,$(PKG_NAME)))
