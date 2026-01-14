cmake_minimum_required(VERSION 3.30)

set(NAME gettext)
set(VERSION 0.26)
set(EXT tar.gz)
set(SHA256 39acf4b0371e9b110b60005562aace5b3631fed9b1bb9ecccfc7f56e58bb1d7f)

project("cmeel-${NAME}" VERSION "${VERSION}")

include(ExternalProject)
ExternalProject_Add(
  ${NAME}
  URL "https://ftpmirror.gnu.org/gnu/${NAME}/${NAME}-${VERSION}.${EXT}"
  URL_HASH "SHA256=${SHA256}"
  DOWNLOAD_EXTRACT_TIMESTAMP ON
  BUILD_IN_SOURCE ON
  CONFIGURE_COMMAND
    "env" "CFLAGS=-Wno-incompatible-pointer-types" "am_cv_func_iconv_works=yes"
    "./configure" "--prefix=${CMAKE_INSTALL_PREFIX}" "--disable-java"
    ${CMEEL_CONFIGURE_OPTIONS}
  BUILD_COMMAND "make"
  # TEST_COMMAND "make" "check"
  INSTALL_COMMAND "make" "install")

# dummy file for install target
install(FILES "README.md" DESTINATION "share/cmeel-${NAME}/")
