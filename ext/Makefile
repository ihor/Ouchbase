srcdir = /Users/ihor/Development/projects/ouchbase/ext
builddir = /Users/ihor/Development/projects/ouchbase/ext
top_srcdir = /Users/ihor/Development/projects/ouchbase/ext
top_builddir = /Users/ihor/Development/projects/ouchbase/ext
EGREP = /usr/bin/grep -E
SED = /usr/bin/sed
CONFIGURE_COMMAND = './configure'
CONFIGURE_OPTIONS =
SHLIB_SUFFIX_NAME = dylib
SHLIB_DL_SUFFIX_NAME = so
ZEND_EXT_TYPE = zend_extension
RE2C = re2c
AWK = awk
shared_objects_ouchbase = ouchbase.lo kernel/main.lo kernel/memory.lo kernel/exception.lo kernel/hash.lo kernel/debug.lo kernel/backtrace.lo kernel/object.lo kernel/array.lo kernel/extended/array.lo kernel/string.lo kernel/fcall.lo kernel/require.lo kernel/file.lo kernel/operators.lo kernel/concat.lo kernel/variables.lo kernel/filter.lo kernel/iterator.lo kernel/exit.lo ouchbase/entity.lo ouchbase/entitymanager.lo ouchbase/entityproxy.lo ouchbase/exception/couchbaseexception.lo ouchbase/exception/entitylogicexception.lo ouchbase/exception/entitymanagerexception.lo ouchbase/exception/entitymodifiedexception.lo ouchbase/exception/entityupdatefailedexception.lo ouchbase/identitymap.lo ouchbase/repository.lo ouchbase/unitofwork.lo ouchbase/_etc.lo
PHP_PECL_EXTENSION = ouchbase
PHP_MODULES = $(phplibdir)/ouchbase.la
PHP_ZEND_EX =
all_targets = $(PHP_MODULES) $(PHP_ZEND_EX)
install_targets = install-modules install-headers
prefix = /usr/local/Cellar/php55/5.5.11
exec_prefix = $(prefix)
libdir = ${exec_prefix}/lib
prefix = /usr/local/Cellar/php55/5.5.11
phplibdir = /Users/ihor/Development/projects/ouchbase/ext/modules
phpincludedir = /usr/local/Cellar/php55/5.5.11/include/php
CC = cc
CFLAGS = -g -O2
CFLAGS_CLEAN = $(CFLAGS)
CPP = cc -E
CPPFLAGS = -DHAVE_CONFIG_H
CXX =
CXXFLAGS =
CXXFLAGS_CLEAN = $(CXXFLAGS)
EXTENSION_DIR = /usr/local/Cellar/php55/5.5.11/lib/php/extensions/no-debug-non-zts-20121212
PHP_EXECUTABLE = /usr/local/Cellar/php55/5.5.11/bin/php
EXTRA_LDFLAGS =
EXTRA_LIBS =
INCLUDES = -I/usr/local/Cellar/php55/5.5.11/include/php -I/usr/local/Cellar/php55/5.5.11/include/php/main -I/usr/local/Cellar/php55/5.5.11/include/php/TSRM -I/usr/local/Cellar/php55/5.5.11/include/php/Zend -I/usr/local/Cellar/php55/5.5.11/include/php/ext -I/usr/local/Cellar/php55/5.5.11/include/php/ext/date/lib
LFLAGS =
LDFLAGS =
SHARED_LIBTOOL =
LIBTOOL = $(SHELL) $(top_builddir)/libtool
SHELL = /bin/sh
INSTALL_HEADERS =
mkinstalldirs = $(top_srcdir)/build/shtool mkdir -p
INSTALL = $(top_srcdir)/build/shtool install -c
INSTALL_DATA = $(INSTALL) -m 644

DEFS = -DPHP_ATOM_INC -I$(top_builddir)/include -I$(top_builddir)/main -I$(top_srcdir)
COMMON_FLAGS = $(DEFS) $(INCLUDES) $(EXTRA_INCLUDES) $(CPPFLAGS) $(PHP_FRAMEWORKPATH)

all: $(all_targets) 
	@echo
	@echo "Build complete."
	@echo "Don't forget to run 'make test'."
	@echo

build-modules: $(PHP_MODULES) $(PHP_ZEND_EX)

build-binaries: $(PHP_BINARIES)

libphp$(PHP_MAJOR_VERSION).la: $(PHP_GLOBAL_OBJS) $(PHP_SAPI_OBJS)
	$(LIBTOOL) --mode=link $(CC) $(CFLAGS) $(EXTRA_CFLAGS) -rpath $(phptempdir) $(EXTRA_LDFLAGS) $(LDFLAGS) $(PHP_RPATHS) $(PHP_GLOBAL_OBJS) $(PHP_SAPI_OBJS) $(EXTRA_LIBS) $(ZEND_EXTRA_LIBS) -o $@
	-@$(LIBTOOL) --silent --mode=install cp $@ $(phptempdir)/$@ >/dev/null 2>&1

libs/libphp$(PHP_MAJOR_VERSION).bundle: $(PHP_GLOBAL_OBJS) $(PHP_SAPI_OBJS)
	$(CC) $(MH_BUNDLE_FLAGS) $(CFLAGS_CLEAN) $(EXTRA_CFLAGS) $(LDFLAGS) $(EXTRA_LDFLAGS) $(PHP_GLOBAL_OBJS:.lo=.o) $(PHP_SAPI_OBJS:.lo=.o) $(PHP_FRAMEWORKS) $(EXTRA_LIBS) $(ZEND_EXTRA_LIBS) -o $@ && cp $@ libs/libphp$(PHP_MAJOR_VERSION).so

install: $(all_targets) $(install_targets)

install-sapi: $(OVERALL_TARGET)
	@echo "Installing PHP SAPI module:       $(PHP_SAPI)"
	-@$(mkinstalldirs) $(INSTALL_ROOT)$(bindir)
	-@if test ! -r $(phptempdir)/libphp$(PHP_MAJOR_VERSION).$(SHLIB_DL_SUFFIX_NAME); then \
		for i in 0.0.0 0.0 0; do \
			if test -r $(phptempdir)/libphp$(PHP_MAJOR_VERSION).$(SHLIB_DL_SUFFIX_NAME).$$i; then \
				$(LN_S) $(phptempdir)/libphp$(PHP_MAJOR_VERSION).$(SHLIB_DL_SUFFIX_NAME).$$i $(phptempdir)/libphp$(PHP_MAJOR_VERSION).$(SHLIB_DL_SUFFIX_NAME); \
				break; \
			fi; \
		done; \
	fi
	@$(INSTALL_IT)

install-binaries: build-binaries $(install_binary_targets)

install-modules: build-modules
	@test -d modules && \
	$(mkinstalldirs) $(INSTALL_ROOT)$(EXTENSION_DIR)
	@echo "Installing shared extensions:     $(INSTALL_ROOT)$(EXTENSION_DIR)/"
	@rm -f modules/*.la >/dev/null 2>&1
	@$(INSTALL) modules/* $(INSTALL_ROOT)$(EXTENSION_DIR)

install-headers:
	-@if test "$(INSTALL_HEADERS)"; then \
		for i in `echo $(INSTALL_HEADERS)`; do \
			i=`$(top_srcdir)/build/shtool path -d $$i`; \
			paths="$$paths $(INSTALL_ROOT)$(phpincludedir)/$$i"; \
		done; \
		$(mkinstalldirs) $$paths && \
		echo "Installing header files:          $(INSTALL_ROOT)$(phpincludedir)/" && \
		for i in `echo $(INSTALL_HEADERS)`; do \
			if test "$(PHP_PECL_EXTENSION)"; then \
				src=`echo $$i | $(SED) -e "s#ext/$(PHP_PECL_EXTENSION)/##g"`; \
			else \
				src=$$i; \
			fi; \
			if test -f "$(top_srcdir)/$$src"; then \
				$(INSTALL_DATA) $(top_srcdir)/$$src $(INSTALL_ROOT)$(phpincludedir)/$$i; \
			elif test -f "$(top_builddir)/$$src"; then \
				$(INSTALL_DATA) $(top_builddir)/$$src $(INSTALL_ROOT)$(phpincludedir)/$$i; \
			else \
				(cd $(top_srcdir)/$$src && $(INSTALL_DATA) *.h $(INSTALL_ROOT)$(phpincludedir)/$$i; \
				cd $(top_builddir)/$$src && $(INSTALL_DATA) *.h $(INSTALL_ROOT)$(phpincludedir)/$$i) 2>/dev/null || true; \
			fi \
		done; \
	fi

PHP_TEST_SETTINGS = -d 'open_basedir=' -d 'output_buffering=0' -d 'memory_limit=-1'
PHP_TEST_SHARED_EXTENSIONS =  ` \
	if test "x$(PHP_MODULES)" != "x"; then \
		for i in $(PHP_MODULES)""; do \
			. $$i; $(top_srcdir)/build/shtool echo -n -- " -d extension=$$dlname"; \
		done; \
	fi; \
	if test "x$(PHP_ZEND_EX)" != "x"; then \
		for i in $(PHP_ZEND_EX)""; do \
			. $$i; $(top_srcdir)/build/shtool echo -n -- " -d $(ZEND_EXT_TYPE)=$(top_builddir)/modules/$$dlname"; \
		done; \
	fi`
PHP_DEPRECATED_DIRECTIVES_REGEX = '^(magic_quotes_(gpc|runtime|sybase)?|(zend_)?extension(_debug)?(_ts)?)[\t\ ]*='

test: all
	@if test ! -z "$(PHP_EXECUTABLE)" && test -x "$(PHP_EXECUTABLE)"; then \
		INI_FILE=`$(PHP_EXECUTABLE) -d 'display_errors=stderr' -r 'echo php_ini_loaded_file();' 2> /dev/null`; \
		if test "$$INI_FILE"; then \
			$(EGREP) -h -v $(PHP_DEPRECATED_DIRECTIVES_REGEX) "$$INI_FILE" > $(top_builddir)/tmp-php.ini; \
		else \
			echo > $(top_builddir)/tmp-php.ini; \
		fi; \
		INI_SCANNED_PATH=`$(PHP_EXECUTABLE) -d 'display_errors=stderr' -r '$$a = explode(",\n", trim(php_ini_scanned_files())); echo $$a[0];' 2> /dev/null`; \
		if test "$$INI_SCANNED_PATH"; then \
			INI_SCANNED_PATH=`$(top_srcdir)/build/shtool path -d $$INI_SCANNED_PATH`; \
			$(EGREP) -h -v $(PHP_DEPRECATED_DIRECTIVES_REGEX) "$$INI_SCANNED_PATH"/*.ini >> $(top_builddir)/tmp-php.ini; \
		fi; \
		TEST_PHP_EXECUTABLE=$(PHP_EXECUTABLE) \
		TEST_PHP_SRCDIR=$(top_srcdir) \
		CC="$(CC)" \
			$(PHP_EXECUTABLE) -n -c $(top_builddir)/tmp-php.ini $(PHP_TEST_SETTINGS) $(top_srcdir)/run-tests.php -n -c $(top_builddir)/tmp-php.ini -d extension_dir=$(top_builddir)/modules/ $(PHP_TEST_SHARED_EXTENSIONS) $(TESTS); \
		TEST_RESULT_EXIT_CODE=$$?; \
		rm $(top_builddir)/tmp-php.ini; \
		exit $$TEST_RESULT_EXIT_CODE; \
	else \
		echo "ERROR: Cannot run tests without CLI sapi."; \
	fi

clean:
	find . -name \*.gcno -o -name \*.gcda | xargs rm -f
	find . -name \*.lo -o -name \*.o | xargs rm -f
	find . -name \*.la -o -name \*.a | xargs rm -f 
	find . -name \*.so | xargs rm -f
	find . -name .libs -a -type d|xargs rm -rf
	rm -f libphp$(PHP_MAJOR_VERSION).la $(SAPI_CLI_PATH) $(SAPI_CGI_PATH) $(SAPI_MILTER_PATH) $(SAPI_LITESPEED_PATH) $(SAPI_FPM_PATH) $(OVERALL_TARGET) modules/* libs/*

distclean: clean
	rm -f Makefile config.cache config.log config.status Makefile.objects Makefile.fragments libtool main/php_config.h main/internal_functions_cli.c main/internal_functions.c stamp-h sapi/apache/libphp$(PHP_MAJOR_VERSION).module sapi/apache_hooks/libphp$(PHP_MAJOR_VERSION).module buildmk.stamp Zend/zend_dtrace_gen.h Zend/zend_dtrace_gen.h.bak Zend/zend_config.h TSRM/tsrm_config.h
	rm -f php5.spec main/build-defs.h scripts/phpize
	rm -f ext/date/lib/timelib_config.h ext/mbstring/oniguruma/config.h ext/mbstring/libmbfl/config.h ext/mysqlnd/php_mysqlnd_config.h
	rm -f scripts/man1/phpize.1 scripts/php-config scripts/man1/php-config.1 sapi/cli/php.1 sapi/cgi/php-cgi.1 ext/phar/phar.1 ext/phar/phar.phar.1
	rm -f sapi/fpm/php-fpm.conf sapi/fpm/init.d.php-fpm sapi/fpm/php-fpm.service sapi/fpm/php-fpm.8 sapi/fpm/status.html
	rm -f ext/iconv/php_have_bsd_iconv.h ext/iconv/php_have_glibc_iconv.h ext/iconv/php_have_ibm_iconv.h ext/iconv/php_have_iconv.h ext/iconv/php_have_libiconv.h ext/iconv/php_iconv_aliased_libiconv.h ext/iconv/php_iconv_supports_errno.h ext/iconv/php_php_iconv_h_path.h ext/iconv/php_php_iconv_impl.h
	rm -f ext/phar/phar.phar ext/phar/phar.php
	if test "$(srcdir)" != "$(builddir)"; then \
	  rm -f ext/phar/phar/phar.inc; \
	fi
	$(EGREP) define'.*include/php' $(top_srcdir)/configure | $(SED) 's/.*>//'|xargs rm -f

.PHONY: all clean install distclean test
.NOEXPORT:
ouchbase.lo: /Users/ihor/Development/projects/ouchbase/ext/ouchbase.c
	$(LIBTOOL) --mode=compile $(CC)  -I. -I/Users/ihor/Development/projects/ouchbase/ext $(COMMON_FLAGS) $(CFLAGS_CLEAN) $(EXTRA_CFLAGS)  -c /Users/ihor/Development/projects/ouchbase/ext/ouchbase.c -o ouchbase.lo 
kernel/main.lo: /Users/ihor/Development/projects/ouchbase/ext/kernel/main.c
	$(LIBTOOL) --mode=compile $(CC)  -I. -I/Users/ihor/Development/projects/ouchbase/ext $(COMMON_FLAGS) $(CFLAGS_CLEAN) $(EXTRA_CFLAGS)  -c /Users/ihor/Development/projects/ouchbase/ext/kernel/main.c -o kernel/main.lo 
kernel/memory.lo: /Users/ihor/Development/projects/ouchbase/ext/kernel/memory.c
	$(LIBTOOL) --mode=compile $(CC)  -I. -I/Users/ihor/Development/projects/ouchbase/ext $(COMMON_FLAGS) $(CFLAGS_CLEAN) $(EXTRA_CFLAGS)  -c /Users/ihor/Development/projects/ouchbase/ext/kernel/memory.c -o kernel/memory.lo 
kernel/exception.lo: /Users/ihor/Development/projects/ouchbase/ext/kernel/exception.c
	$(LIBTOOL) --mode=compile $(CC)  -I. -I/Users/ihor/Development/projects/ouchbase/ext $(COMMON_FLAGS) $(CFLAGS_CLEAN) $(EXTRA_CFLAGS)  -c /Users/ihor/Development/projects/ouchbase/ext/kernel/exception.c -o kernel/exception.lo 
kernel/hash.lo: /Users/ihor/Development/projects/ouchbase/ext/kernel/hash.c
	$(LIBTOOL) --mode=compile $(CC)  -I. -I/Users/ihor/Development/projects/ouchbase/ext $(COMMON_FLAGS) $(CFLAGS_CLEAN) $(EXTRA_CFLAGS)  -c /Users/ihor/Development/projects/ouchbase/ext/kernel/hash.c -o kernel/hash.lo 
kernel/debug.lo: /Users/ihor/Development/projects/ouchbase/ext/kernel/debug.c
	$(LIBTOOL) --mode=compile $(CC)  -I. -I/Users/ihor/Development/projects/ouchbase/ext $(COMMON_FLAGS) $(CFLAGS_CLEAN) $(EXTRA_CFLAGS)  -c /Users/ihor/Development/projects/ouchbase/ext/kernel/debug.c -o kernel/debug.lo 
kernel/backtrace.lo: /Users/ihor/Development/projects/ouchbase/ext/kernel/backtrace.c
	$(LIBTOOL) --mode=compile $(CC)  -I. -I/Users/ihor/Development/projects/ouchbase/ext $(COMMON_FLAGS) $(CFLAGS_CLEAN) $(EXTRA_CFLAGS)  -c /Users/ihor/Development/projects/ouchbase/ext/kernel/backtrace.c -o kernel/backtrace.lo 
kernel/object.lo: /Users/ihor/Development/projects/ouchbase/ext/kernel/object.c
	$(LIBTOOL) --mode=compile $(CC)  -I. -I/Users/ihor/Development/projects/ouchbase/ext $(COMMON_FLAGS) $(CFLAGS_CLEAN) $(EXTRA_CFLAGS)  -c /Users/ihor/Development/projects/ouchbase/ext/kernel/object.c -o kernel/object.lo 
kernel/array.lo: /Users/ihor/Development/projects/ouchbase/ext/kernel/array.c
	$(LIBTOOL) --mode=compile $(CC)  -I. -I/Users/ihor/Development/projects/ouchbase/ext $(COMMON_FLAGS) $(CFLAGS_CLEAN) $(EXTRA_CFLAGS)  -c /Users/ihor/Development/projects/ouchbase/ext/kernel/array.c -o kernel/array.lo 
kernel/extended/array.lo: /Users/ihor/Development/projects/ouchbase/ext/kernel/extended/array.c
	$(LIBTOOL) --mode=compile $(CC)  -I. -I/Users/ihor/Development/projects/ouchbase/ext $(COMMON_FLAGS) $(CFLAGS_CLEAN) $(EXTRA_CFLAGS)  -c /Users/ihor/Development/projects/ouchbase/ext/kernel/extended/array.c -o kernel/extended/array.lo 
kernel/string.lo: /Users/ihor/Development/projects/ouchbase/ext/kernel/string.c
	$(LIBTOOL) --mode=compile $(CC)  -I. -I/Users/ihor/Development/projects/ouchbase/ext $(COMMON_FLAGS) $(CFLAGS_CLEAN) $(EXTRA_CFLAGS)  -c /Users/ihor/Development/projects/ouchbase/ext/kernel/string.c -o kernel/string.lo 
kernel/fcall.lo: /Users/ihor/Development/projects/ouchbase/ext/kernel/fcall.c
	$(LIBTOOL) --mode=compile $(CC)  -I. -I/Users/ihor/Development/projects/ouchbase/ext $(COMMON_FLAGS) $(CFLAGS_CLEAN) $(EXTRA_CFLAGS)  -c /Users/ihor/Development/projects/ouchbase/ext/kernel/fcall.c -o kernel/fcall.lo 
kernel/require.lo: /Users/ihor/Development/projects/ouchbase/ext/kernel/require.c
	$(LIBTOOL) --mode=compile $(CC)  -I. -I/Users/ihor/Development/projects/ouchbase/ext $(COMMON_FLAGS) $(CFLAGS_CLEAN) $(EXTRA_CFLAGS)  -c /Users/ihor/Development/projects/ouchbase/ext/kernel/require.c -o kernel/require.lo 
kernel/file.lo: /Users/ihor/Development/projects/ouchbase/ext/kernel/file.c
	$(LIBTOOL) --mode=compile $(CC)  -I. -I/Users/ihor/Development/projects/ouchbase/ext $(COMMON_FLAGS) $(CFLAGS_CLEAN) $(EXTRA_CFLAGS)  -c /Users/ihor/Development/projects/ouchbase/ext/kernel/file.c -o kernel/file.lo 
kernel/operators.lo: /Users/ihor/Development/projects/ouchbase/ext/kernel/operators.c
	$(LIBTOOL) --mode=compile $(CC)  -I. -I/Users/ihor/Development/projects/ouchbase/ext $(COMMON_FLAGS) $(CFLAGS_CLEAN) $(EXTRA_CFLAGS)  -c /Users/ihor/Development/projects/ouchbase/ext/kernel/operators.c -o kernel/operators.lo 
kernel/concat.lo: /Users/ihor/Development/projects/ouchbase/ext/kernel/concat.c
	$(LIBTOOL) --mode=compile $(CC)  -I. -I/Users/ihor/Development/projects/ouchbase/ext $(COMMON_FLAGS) $(CFLAGS_CLEAN) $(EXTRA_CFLAGS)  -c /Users/ihor/Development/projects/ouchbase/ext/kernel/concat.c -o kernel/concat.lo 
kernel/variables.lo: /Users/ihor/Development/projects/ouchbase/ext/kernel/variables.c
	$(LIBTOOL) --mode=compile $(CC)  -I. -I/Users/ihor/Development/projects/ouchbase/ext $(COMMON_FLAGS) $(CFLAGS_CLEAN) $(EXTRA_CFLAGS)  -c /Users/ihor/Development/projects/ouchbase/ext/kernel/variables.c -o kernel/variables.lo 
kernel/filter.lo: /Users/ihor/Development/projects/ouchbase/ext/kernel/filter.c
	$(LIBTOOL) --mode=compile $(CC)  -I. -I/Users/ihor/Development/projects/ouchbase/ext $(COMMON_FLAGS) $(CFLAGS_CLEAN) $(EXTRA_CFLAGS)  -c /Users/ihor/Development/projects/ouchbase/ext/kernel/filter.c -o kernel/filter.lo 
kernel/iterator.lo: /Users/ihor/Development/projects/ouchbase/ext/kernel/iterator.c
	$(LIBTOOL) --mode=compile $(CC)  -I. -I/Users/ihor/Development/projects/ouchbase/ext $(COMMON_FLAGS) $(CFLAGS_CLEAN) $(EXTRA_CFLAGS)  -c /Users/ihor/Development/projects/ouchbase/ext/kernel/iterator.c -o kernel/iterator.lo 
kernel/exit.lo: /Users/ihor/Development/projects/ouchbase/ext/kernel/exit.c
	$(LIBTOOL) --mode=compile $(CC)  -I. -I/Users/ihor/Development/projects/ouchbase/ext $(COMMON_FLAGS) $(CFLAGS_CLEAN) $(EXTRA_CFLAGS)  -c /Users/ihor/Development/projects/ouchbase/ext/kernel/exit.c -o kernel/exit.lo 
ouchbase/entity.lo: /Users/ihor/Development/projects/ouchbase/ext/ouchbase/entity.zep.c
	$(LIBTOOL) --mode=compile $(CC)  -I. -I/Users/ihor/Development/projects/ouchbase/ext $(COMMON_FLAGS) $(CFLAGS_CLEAN) $(EXTRA_CFLAGS)  -c /Users/ihor/Development/projects/ouchbase/ext/ouchbase/entity.zep.c -o ouchbase/entity.lo 
ouchbase/entitymanager.lo: /Users/ihor/Development/projects/ouchbase/ext/ouchbase/entitymanager.zep.c
	$(LIBTOOL) --mode=compile $(CC)  -I. -I/Users/ihor/Development/projects/ouchbase/ext $(COMMON_FLAGS) $(CFLAGS_CLEAN) $(EXTRA_CFLAGS)  -c /Users/ihor/Development/projects/ouchbase/ext/ouchbase/entitymanager.zep.c -o ouchbase/entitymanager.lo 
ouchbase/entityproxy.lo: /Users/ihor/Development/projects/ouchbase/ext/ouchbase/entityproxy.zep.c
	$(LIBTOOL) --mode=compile $(CC)  -I. -I/Users/ihor/Development/projects/ouchbase/ext $(COMMON_FLAGS) $(CFLAGS_CLEAN) $(EXTRA_CFLAGS)  -c /Users/ihor/Development/projects/ouchbase/ext/ouchbase/entityproxy.zep.c -o ouchbase/entityproxy.lo 
ouchbase/exception/couchbaseexception.lo: /Users/ihor/Development/projects/ouchbase/ext/ouchbase/exception/couchbaseexception.zep.c
	$(LIBTOOL) --mode=compile $(CC)  -I. -I/Users/ihor/Development/projects/ouchbase/ext $(COMMON_FLAGS) $(CFLAGS_CLEAN) $(EXTRA_CFLAGS)  -c /Users/ihor/Development/projects/ouchbase/ext/ouchbase/exception/couchbaseexception.zep.c -o ouchbase/exception/couchbaseexception.lo 
ouchbase/exception/entitylogicexception.lo: /Users/ihor/Development/projects/ouchbase/ext/ouchbase/exception/entitylogicexception.zep.c
	$(LIBTOOL) --mode=compile $(CC)  -I. -I/Users/ihor/Development/projects/ouchbase/ext $(COMMON_FLAGS) $(CFLAGS_CLEAN) $(EXTRA_CFLAGS)  -c /Users/ihor/Development/projects/ouchbase/ext/ouchbase/exception/entitylogicexception.zep.c -o ouchbase/exception/entitylogicexception.lo 
ouchbase/exception/entitymanagerexception.lo: /Users/ihor/Development/projects/ouchbase/ext/ouchbase/exception/entitymanagerexception.zep.c
	$(LIBTOOL) --mode=compile $(CC)  -I. -I/Users/ihor/Development/projects/ouchbase/ext $(COMMON_FLAGS) $(CFLAGS_CLEAN) $(EXTRA_CFLAGS)  -c /Users/ihor/Development/projects/ouchbase/ext/ouchbase/exception/entitymanagerexception.zep.c -o ouchbase/exception/entitymanagerexception.lo 
ouchbase/exception/entitymodifiedexception.lo: /Users/ihor/Development/projects/ouchbase/ext/ouchbase/exception/entitymodifiedexception.zep.c
	$(LIBTOOL) --mode=compile $(CC)  -I. -I/Users/ihor/Development/projects/ouchbase/ext $(COMMON_FLAGS) $(CFLAGS_CLEAN) $(EXTRA_CFLAGS)  -c /Users/ihor/Development/projects/ouchbase/ext/ouchbase/exception/entitymodifiedexception.zep.c -o ouchbase/exception/entitymodifiedexception.lo 
ouchbase/exception/entityupdatefailedexception.lo: /Users/ihor/Development/projects/ouchbase/ext/ouchbase/exception/entityupdatefailedexception.zep.c
	$(LIBTOOL) --mode=compile $(CC)  -I. -I/Users/ihor/Development/projects/ouchbase/ext $(COMMON_FLAGS) $(CFLAGS_CLEAN) $(EXTRA_CFLAGS)  -c /Users/ihor/Development/projects/ouchbase/ext/ouchbase/exception/entityupdatefailedexception.zep.c -o ouchbase/exception/entityupdatefailedexception.lo 
ouchbase/identitymap.lo: /Users/ihor/Development/projects/ouchbase/ext/ouchbase/identitymap.zep.c
	$(LIBTOOL) --mode=compile $(CC)  -I. -I/Users/ihor/Development/projects/ouchbase/ext $(COMMON_FLAGS) $(CFLAGS_CLEAN) $(EXTRA_CFLAGS)  -c /Users/ihor/Development/projects/ouchbase/ext/ouchbase/identitymap.zep.c -o ouchbase/identitymap.lo 
ouchbase/repository.lo: /Users/ihor/Development/projects/ouchbase/ext/ouchbase/repository.zep.c
	$(LIBTOOL) --mode=compile $(CC)  -I. -I/Users/ihor/Development/projects/ouchbase/ext $(COMMON_FLAGS) $(CFLAGS_CLEAN) $(EXTRA_CFLAGS)  -c /Users/ihor/Development/projects/ouchbase/ext/ouchbase/repository.zep.c -o ouchbase/repository.lo 
ouchbase/unitofwork.lo: /Users/ihor/Development/projects/ouchbase/ext/ouchbase/unitofwork.zep.c
	$(LIBTOOL) --mode=compile $(CC)  -I. -I/Users/ihor/Development/projects/ouchbase/ext $(COMMON_FLAGS) $(CFLAGS_CLEAN) $(EXTRA_CFLAGS)  -c /Users/ihor/Development/projects/ouchbase/ext/ouchbase/unitofwork.zep.c -o ouchbase/unitofwork.lo 
ouchbase/_etc.lo: /Users/ihor/Development/projects/ouchbase/ext/ouchbase/_etc.zep.c
	$(LIBTOOL) --mode=compile $(CC)  -I. -I/Users/ihor/Development/projects/ouchbase/ext $(COMMON_FLAGS) $(CFLAGS_CLEAN) $(EXTRA_CFLAGS)  -c /Users/ihor/Development/projects/ouchbase/ext/ouchbase/_etc.zep.c -o ouchbase/_etc.lo 
$(phplibdir)/ouchbase.la: ./ouchbase.la
	$(LIBTOOL) --mode=install cp ./ouchbase.la $(phplibdir)

./ouchbase.la: $(shared_objects_ouchbase) $(OUCHBASE_SHARED_DEPENDENCIES)
	$(LIBTOOL) --mode=link $(CC) $(COMMON_FLAGS) $(CFLAGS_CLEAN) $(EXTRA_CFLAGS) $(LDFLAGS) -o $@ -export-dynamic -avoid-version -prefer-pic -module -rpath $(phplibdir) $(EXTRA_LDFLAGS) $(shared_objects_ouchbase) $(OUCHBASE_SHARED_LIBADD)

