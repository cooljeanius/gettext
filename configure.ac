dnl Configuration for the toplevel directory of GNU gettext
dnl Copyright (C) 1995-1999, 2000-2003, 2005-2006, 2009-2010 Free Software Foundation, Inc.
dnl
dnl This program is free software: you can redistribute it and/or modify
dnl it under the terms of the GNU General Public License as published by
dnl the Free Software Foundation; either version 3 of the License, or
dnl (at your option) any later version.
dnl
dnl This program is distributed in the hope that it will be useful,
dnl but WITHOUT ANY WARRANTY; without even the implied warranty of
dnl MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
dnl GNU General Public License for more details.
dnl
dnl You should have received a copy of the GNU General Public License
dnl along with this program.  If not, see <http://www.gnu.org/licenses/>.

dnl Process this file with autoconf to produce a configure script.

AC_PREREQ([2.59])
AC_INIT([gettext], [0.18.2])
AC_CONFIG_SRCDIR([gettext-tools/src/msgfmt.c])
AC_CONFIG_AUX_DIR([build-aux])
AC_CONFIG_HEADERS([config.h])
gl_SYS_TYPES_H_REQUIRER
. $srcdir/version.sh
gl_INIT_PACKAGE([gettext], [$VERSION_NUMBER])
AM_INIT_AUTOMAKE([silent-rules])
AM_MAINTAINER_MODE
AM_WITH_REGEX
AC_USE_SYSTEM_EXTENSIONS

dnl Override automake's tar command used for creating distributions.
am__tar='${AMTAR} chof - --owner=root --group=root "$$tardir"'

dnl Checks for programs.
AC_PROG_CXX
AC_PROG_AWK
AC_PROG_YACC
AC_PROG_CC
AM_PROG_CC_C_O
AC_PROG_CPP
AC_PROG_INSTALL
AC_PROG_LN_S
AC_PROG_MAKE_SET
AC_PROG_RANLIB

dnl Checks for libraries.
# FIXME: Replace `main' with a function in `-lgcc':
AC_CHECK_LIB([gcc], [main])
# FIXME: Replace `main' with a function in `-liberty':
AC_CHECK_LIB([iberty], [main])
# FIXME: Replace `main' with a function in `-liconv':
AC_CHECK_LIB([iconv], [main])

dnl Checks for header files.
AC_HEADER_STDC
AC_FUNC_ALLOCA
AC_HEADER_RESOLV
AC_CHECK_HEADERS([OS.h arpa/inet.h fcntl.h float.h libintl.h limits.h locale.h malloc.h netdb.h netinet/in.h stddef.h stdint.h stdio.h stdlib.h string.h strings.h sys/socket.h sys/time.h unistd.h])

dnl Checks for typedefs, structures, and compiler characteristics.
AC_CHECK_HEADER_STDBOOL
AC_TYPE_UID_T
AC_C_INLINE
AC_FUNC_OBSTACK
AC_TYPE_SIZE_T
AC_TYPE_SSIZE_T
AC_CHECK_DECLS([sys_siglist])
AC_TYPE_UINT16_T
AC_TYPE_UINT32_T
AC_CHECK_TYPES([ptrdiff_t])

dnl Checks for library functions.
AM_GNU_GETTEXT([external])
AC_FUNC_ERROR_AT_LINE
AC_FUNC_MALLOC
AC_FUNC_REALLOC
AC_FUNC_STRTOD
AC_CHECK_FUNCS([atexit endpwent getcwd gethostbyname getwd localeconv memchr memmove memset pathconf pow putenv select socket stpcpy strcasecmp strchr strerror strncasecmp strpbrk strstr strtol])


AC_CONFIG_SUBDIRS([gettext-runtime gettext-tools])

dnl Ensure that "configure --help" lists all the command line options that
dnl are usable with the subdir configures. Really AC_CONFIG_SUBDIRS should
dnl do it by itself.
dnl System types:
AC_CANONICAL_HOST
dnl Optional Features: AC_ARG_ENABLE calls
dnl Optional Packages: AC_ARG_WITH calls
dnl Some influential environment variables: AC_ARG_VAR calls
esyscmd([{ cd gettext-runtime && autoconf --trace=AC_ARG_ENABLE:'$n([$1],[$2])' --trace=AC_ARG_WITH:'$n([$1],[$2])' --trace=AC_ARG_VAR:'$n($@)' && cd ..; cd gettext-tools && autoconf --trace=AC_ARG_ENABLE:'$n([$1],[$2])' --trace=AC_ARG_WITH:'$n([$1],[$2])' --trace=AC_ARG_VAR:'$n($@)' && cd ..; } | sed -f build-aux/ac-help.sed ])

AC_CONFIG_FILES([Makefile po/Makefile.in])

AC_CONFIG_FILES([gnulib-local/Makefile])

AC_OUTPUT
