SRC_NAME=htop-2.0.2

THISDIR = $(shell pwd)

all: config_test
	$(MAKE) -C $(SRC_NAME)

config_test:
	( if [ -f ./config_done ]; then \
		echo "the same configuration"; \
	else \
		make configure && touch config_done; \
	fi )

configure:
	( cd $(SRC_NAME) ; \
	./configure \
		--host=$(HOST_TARGET) \
		--build=$(HOST_BUILD) \
		--disable-hwloc \
	)

clean:
	$(MAKE) -C $(SRC_NAME) distclean
	rm -f config_done

romfs:
	$(ROMFSINST) $(THISDIR)/$(SRC_NAME)/htop /bin/htop

