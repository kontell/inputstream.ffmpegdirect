cmake_minimum_required(VERSION 3.5)
project(iconv)

if(AUTOTOOLS_HOST)
  set(ICONV_CROSS_ARGS --host=${AUTOTOOLS_HOST})
endif()

include(ExternalProject)
externalproject_add(iconv
                    SOURCE_DIR ${CMAKE_SOURCE_DIR}
                    CONFIGURE_COMMAND ./configure
                      --prefix=${OUTPUT_DIR}
                      --without-libiconv-prefix
                      --without-libintl-prefix
                      --disable-debug
                      --disable-shared
                      --disable-dependency-tracking
                      --disable-nls
                      --enable-extra-encodings
                      --enable-static
                      --with-pic
                      ${ICONV_CROSS_ARGS}
                    BUILD_COMMAND make
                    INSTALL_COMMAND ""
                    BUILD_IN_SOURCE 1)

install(CODE "execute_process(COMMAND make install-lib WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR})")
