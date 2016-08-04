SRC_NAME=tinc-1.1x

CFLAGS  += -std=gnu99 -ffunction-sections -fdata-sections
CXXFLAGS += -ffunction-sections -fdata-sections
LDFLAGS += -Wl,--gc-sections

THISDIR = $(shell pwd)

all: config_test
	$(MAKE) -C $(SRC_NAME) install DESTDIR=$(THISDIR)/install

config_test:
	( if [ -f ./config_done ]; then \
		echo "the same configuration"; \
	else \
		make configure && touch config_done; \
	fi )

configure:
	( cd $(SRC_NAME) ; \
	./configure \
		--prefix=/usr \
		--sysconfdir=/etc/storage \
		--host=$(HOST_TARGET) \
		--build=$(HOST_BUILD) \
		--disable-curses \
		--disable-readline \
		--with-zlib="$(STAGEDIR)" \
		--with-lzo-include="$(STAGEDIR)/include/lzo" ; \
	)

clean:
	rm -f config_done
	rm -rf install

romfs:
	$(ROMFSINST) $(THISDIR)/install/usr/sbin/tinc /usr/sbin
	$(ROMFSINST) $(THISDIR)/install/usr/sbin/tincd /usr/sbin
