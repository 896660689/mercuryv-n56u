SRC_NAME=ncurses-6.0

CFLAGS  += -Os -fPIC
LDFLAGS += -ffunction-sections -fdata-sections

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
		--prefix="" \
		--host=$(HOST_TARGET) \
		--build=$(HOST_BUILD) \
		--without-cxx \
		--without-cxx-binding \
		--enable-echo \
		--enable-const \
		--enable-overwrite \
		--disable-rpath \
		--without-ada \
		--enable-widec \
		--without-debug \
		--without-manpages \
		--without-profile \
		--without-progs \
		--without-tests \
		--disable-home-terminfo \
		--disable-normal \
		--with-shared \
		--with-build-cppflags=-D_GNU_SOURCE \
		--disable-termcap \
		--disable-database \
		--with-fallbacks="xterm,vt100,vt200,linux,ansi" \
	)

install:
	$(MAKE) -C $(SRC_NAME) install.libs DESTDIR="$(STAGEDIR)"
	ln -s $(STAGEDIR)/include/curses.h $(STAGEDIR)/include/ncursesw.h

clean:
	$(MAKE) -C $(SRC_NAME) distclean
	rm -f config_done

romfs:
	cp -fP $(DESTDIR)/lib/libncursesw.so* $(ROMFSDIR)/lib
