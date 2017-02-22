SRC_NAME=dnscrypt-proxy-1.9.4

CFLAGS  += -ffunction-sections -fdata-sections
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
	./autogen.sh ; \
	./configure \
		--prefix=/usr \
		--host=$(HOST_TARGET) \
		--build=$(HOST_BUILD) \
		--disable-ssp \
		--disable-plugins ; \
	)

clean:
	rm -f config_done
	rm -rf install

romfs:
	$(ROMFSINST) $(THISDIR)/install/usr/sbin/dnscrypt-proxy /usr/sbin/dnscrypt-proxy
	cp -fr $(THISDIR)/install/usr/share $(INSTALLDIR)/usr
