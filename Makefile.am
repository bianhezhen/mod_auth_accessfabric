ACLOCAL_AMFLAGS = -I m4

AUTOMAKE_OPTIONS = foreign

dist_doc_DATA = README.md NOTICE LICENSE CONTRIBUTING.md CODE_OF_CONDUCT.md

EXTRA_DIST = .clang-format \
    buildconf.sh \
    ./scripts/test-build.sh

lib_LTLIBRARIES = mod_auth_accessfabric.la

# we override install, so that we don't also install the .so into /usr/local
install: all-am
	@$(MAKE) $(AM_MAKEFLAGS) install-apxs install-data

install-apxs: mod_auth_accessfabric.la
	$(MKDIR_P) $(DESTDIR)/@LIBEXEC_DIR@
	$(APXS) -i -S LIBEXECDIR=$(DESTDIR)/@LIBEXEC_DIR@ -n auth_accessfabric mod_auth_accessfabric.la

mod_auth_accessfabric_la_SOURCES = src/af_fetch.c \
    src/af_types.h \
    src/af_cache.h \
    src/mod_auth_accessfabric.c \
    src/af_fetch.h \
    src/af_cache.c

mod_auth_accessfabric_la_LDFLAGS = -avoid-version -module -shared

CLANG_FORMAT = clang-format
CLANG_FORMAT_OPTIONS = -style=file -i

format: $(mod_auth_accessfabric_la_SOURCES) $(HEADERS)
	$(CLANG_FORMAT) $(CLANG_FORMAT_OPTIONS) $(mod_auth_accessfabric_la_SOURCES) $(HEADERS)

.PHONY: format
