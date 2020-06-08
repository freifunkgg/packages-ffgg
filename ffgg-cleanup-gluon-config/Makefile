include $(TOPDIR)/rules.mk

PKG_NAME:=cleanup-gluon-config
PKG_VERSION:=1

include $(TOPDIR)/../package/gluon.mk

define Package/$(PKG_NAME)
  TITLE:=Cleanup and wipe the Gluon config but reuse older user changes
  DEPENDS:=+gluon-core
endef

$(eval $(call BuildPackageGluon,$(PKG_NAME)))

