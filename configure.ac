AC_INIT([toml], [1.0])

AC_LANG_C
AC_LANG_WERROR
AC_PROG_CC([clang cc gcc])

AC_CHECK_PROG([RAGEL], [ragel], [yes])
if test "x$RAGEL" != "xyes"
then
	exit 1
fi

LDFLAGS="$LDFLAGS -L."

AC_ARG_WITH(cunit, [--with-cunit=<path> cunit path for tests],
	[
		case "$withval" in
		"yes")
			AC_CHECK_LIB([cunit], [CU_get_error],,
											AC_MSG_ERROR([cunit not found]))
			;;
		*)
			savedCFLAGS=$CFLAGS
			savedLDFLAGS=$LDFLAGS
			CFLAGS="$CFLAGS -I$withval/include"
			LDFLAGS="$LDFLAGS -L$withval/lib"
			AC_CHECK_LIB([cunit], [CU_get_error], [
				AC_CHECK_HEADER([CUnit/CUnit.h], [
					savedCFLAGS=$CFLAGS
					savedLDFLAGS="$LDFLAGS"
				])
			])
			CFLAGS=$savedCFLAGS
			LDFLAGS=$savedLDFLAGS
			;;
		esac
	]
)

AC_CONFIG_FILES([Makefile])
AC_OUTPUT
