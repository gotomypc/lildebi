
PKG_NAME:=debian-archive-keyring
PKG_VERSION:=2012.4

PKG_SOURCE:=$(PKG_NAME)_$(PKG_VERSION)_all.deb
PKG_SOURCE_URL:=https://mirrors.kernel.org/debian/pool/main/d/debian-archive-keyring

DL_DIR=$(PKG_NAME)-$(PKG_VERSION)

compare: $(DL_DIR)/usr/share/keyrings/debian-archive-keyring.gpg
	diff ../../assets/debian-archive-keyring.gpg \
		$(DL_DIR)/usr/share/keyrings/debian-archive-keyring.gpg

$(DL_DIR)/usr/share/keyrings/debian-archive-keyring.gpg: $(DL_DIR)/$(PKG_SOURCE)
	cd $(DL_DIR) && \
		(ar -p $(PKG_SOURCE) data.tar.gz | \
			tar --preserve-permissions --extract --gunzip --file - )

$(DL_DIR)/$(PKG_SOURCE): $(DL_DIR)
	cd $(DL_DIR) && \
		wget --continue $(PKG_SOURCE_URL)/$(PKG_SOURCE)
	md5sum -c $(PKG_SOURCE).md5
	sha1sum -c $(PKG_SOURCE).sha1
	sha256sum -c $(PKG_SOURCE).sha256

$(DL_DIR):
	mkdir $(DL_DIR)


clean:
	-rm -rf -- $(DL_DIR)
	-rm -f -- debian-archive-keyring.gpg

.PHONY: clean compare
