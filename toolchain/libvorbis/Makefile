NAME     = libvorbis
TITLE    = libvorbis
APP_ID   = org.webosinternals.toolchain.${NAME}
SRC_VER  = 1.3.2
VERSION  = 1.3.2-1
MAINTAINER = WebOS Internals <support@webos-internals.org>

SRC_TGZ = http://downloads.xiph.org/releases/vorbis/${NAME}-${SRC_VER}.tar.gz

.PHONY: package
package: build/.built-${VERSION}

include ../../support/download.mk

.PHONY: stage
stage: build/.staged-${VERSION}

build/.staged-${VERSION}: build/armv7.staged-${VERSION} build/armv6.staged-${VERSION} build/i686.staged-${VERSION}
	touch $@

build/%.staged-${VERSION} : build/%.built-${VERSION}
	mkdir -p ../../staging/$*/usr/include
	cp -rp build/$*/usr/include/* ../../staging/$*/usr/include/
	mkdir -p ../../staging/$*/usr/lib
	cp -rp build/$*/usr/lib/* ../../staging/$*/usr/lib/
	touch $@

.PHONY: unpack
unpack: build/.unpacked-${VERSION}

build/.unpacked-${VERSION}: ${DL_DIR}/${NAME}-${VERSION}.tar.gz
	rm -rf build
	mkdir -p build/armv6 build/armv7 build/i686
	tar -C build -z -x -f $<
	mv build/${NAME}-${SRC_VER} build/src
	touch $@

.PHONY: build
build: build/.built-${VERSION}

build/.built-${VERSION}: build/armv7.built-${VERSION} build/armv6.built-${VERSION} build/i686.built-${VERSION}
	touch $@

include ../../support/cross-compile.mk

build/%.built-${VERSION}: build/.unpacked-${VERSION}
	rm -rf build/$*
	( cd build/src ; \
	  CFLAGS="-I${STAGING_DIR_$*}/usr/include" \
	  LDFLAGS="-L${STAGING_DIR_$*}/usr/lib" \
	  CC=${CROSS_COMPILE_$*}gcc \
	  ./configure \
	  	--host=${CONFIGURE_HOST_$*} \
	  	--disable-static ; \
	  ${MAKE} clean all )
	mkdir -p build/$*/usr/include/vorbis
	install -m 644 build/src/include/vorbis/*.h build/$*/usr/include/vorbis
	mkdir -p build/$*/usr/lib
	install -m 755 build/src/lib/.libs/*.so* build/$*/usr/lib/
	touch $@

clobber::
	rm -rf build
