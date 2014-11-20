AC_PREREQ([2.65])
AC_INIT([pax-utils], [git])
AC_CONFIG_AUX_DIR([autotools])
AM_INIT_AUTOMAKE([1.11 dist-xz no-dist-gzip silent-rules -Wall])
AM_SILENT_RULES([yes]) # AM_INIT_AUTOMAKE([silent-rules]) is broken atm
AC_CONFIG_HEADER([config.h])
AC_CONFIG_MACRO_DIR([autotools/m4])

AC_PROG_CC_C99
AM_PROG_CC_C_O
AM_PROG_AR
AC_USE_SYSTEM_EXTENSIONS
LT_INIT

gl_EARLY
gl_INIT

AC_ARG_WITH([caps], [AS_HELP_STRING([--with-caps], [build with capabilities])])
AS_IF([test "x$with_caps" = "xyes"], [
	CPPFLAGS="$CPPFLAGS -DWANT_SYSCAP"
	LIBS="$LIBS -lcap"
])

AC_ARG_WITH([python], [AS_HELP_STRING([--with-python], [use lddtree.py])])
AM_CONDITIONAL([USE_PYTHON], [test "x$with_python" = "xyes"])

AX_CFLAGS_WARN_ALL
AC_DEFUN([PT_CHECK_CFLAG],[AX_CHECK_COMPILER_FLAGS([$1],[CFLAGS="$CFLAGS $1"])])
m4_foreach_w([flag], [
	-Wunused
	-Wimplicit
	-Wshadow
	-Wformat=2
	-Wmissing-declarations
	-Wno-missing-prototypes
	-Wwrite-strings
	-Wbad-function-cast
	-Wnested-externs
	-Wcomment
	-Winline
	-Wchar-subscripts
	-Wcast-align
	-Wno-format-nonliteral
	-Wsequence-point
	-Wold-style-definition
	-Wextra
], [
	AX_CHECK_COMPILE_FLAG(flag, AS_VAR_APPEND([CFLAGS], " flag"))
])

AC_CONFIG_FILES([
	Makefile
	autotools/gnulib/Makefile
])
AC_OUTPUT