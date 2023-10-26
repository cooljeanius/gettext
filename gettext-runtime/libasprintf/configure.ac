dnl# Configuration for the GNU libasprintf library
dnl# Copyright (C) 2002-2011 Free Software Foundation, Inc.
dnl#
dnl# This program is free software: you can redistribute it and/or modify
dnl# it under the terms of the GNU General Public License as published by
dnl# the Free Software Foundation; either version 3 of the License, or
dnl# (at your option) any later version.
dnl#
dnl# This program is distributed in the hope that it will be useful,
dnl# but WITHOUT ANY WARRANTY; without even the implied warranty of
dnl# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
dnl# GNU General Public License for more details.
dnl#
dnl# You should have received a copy of the GNU General Public License
dnl# along with this program.  If not, see <http://www.gnu.org/licenses/>.

dnl# Process this file with autoconf to produce a configure script.

AC_PREREQ([2.70])
AC_INIT([libasprintf],[1.0],[ueno@gnu.org],[libasprintf],
        [https://www.gnu.org/software/gettext/])
AC_CONFIG_SRCDIR([vasprintf.c])
AC_CONFIG_AUX_DIR([../../build-aux])
AC_CONFIG_MACRO_DIR([../../m4])
AM_INIT_AUTOMAKE([1.5 gnu no-dependencies silent-rules])
AC_CONFIG_HEADERS([config.h])
AM_MAINTAINER_MODE
AC_USE_SYSTEM_EXTENSIONS

dnl# Checks for programs.
AC_PROG_CC
AM_PROG_CC_C_O
AC_PROG_CPP
AC_PROG_CXX
AC_PROG_INSTALL

dnl# Check for host type.
AC_CANONICAL_HOST

dnl# Checks for compiler output filename suffixes.
AC_OBJEXT
AC_EXEEXT

dnl# Early checks, assembled by gnulib.
gl_EARLY

dnl# Check for build configuration.
gl_WOE32_DLL
LT_INIT([win32-dll])
case "$host_os" in
  # On Cygwin, without -no-undefined, a warning is emitted and only a static
  # library is built.
  beos* | mingw* | cygwin*) LTNOUNDEF='-no-undefined' ;;
  *) LTNOUNDEF='' ;;
esac
AC_SUBST([LTNOUNDEF])dnl

dnl Checks for libraries.

dnl# Checks for header files.
AC_FUNC_ALLOCA
dnl# autoupdate says:
dnl# The preprocessor macro `STDC_HEADERS' is obsolete.
dnl# Except in unusual embedded environments, you can safely include all
dnl# ISO C90 headers unconditionally.
# Autoupdate added the next two lines to ensure that your configure
# script's behavior did not change.  They are probably safe to remove.
AC_CHECK_INCLUDES_DEFAULT
if test "x${EGREP}" = "x"; then
  test -z "${EGREP}"
  AC_PROG_EGREP
fi
AC_CHECK_HEADERS([float.h inttypes.h langinfo.h limits.h locale.h malloc.h stddef.h stdint.h stdio.h stdlib.h string.h wchar.h])
AC_CHECK_HEADERS([features.h])dnl

dnl# Checks for typedefs, structures, and compiler characteristics.
AC_C_INLINE
AC_TYPE_SIZE_T
AC_TYPE_LONG_LONG_INT
gt_TYPE_WCHAR_T
gt_TYPE_WINT_T
AC_TYPE_MBSTATE_T
AC_TYPE_UINT16_T
AC_TYPE_UINT32_T
AC_TYPE_UINT8_T
AC_CHECK_TYPE([ptrdiff_t],[],
  [AC_DEFINE([ptrdiff_t],[long],
     [Define as the type of the result of subtracting two pointers, if the system doesn't define it.])
  ])
gl_AC_TYPE_INTMAX_T
gl_XSIZE

dnl# Checks for library functions.
AC_FUNC_MALLOC
AC_FUNC_MBRTOWC
AC_FUNC_REALLOC
AC_CHECK_FUNCS([localeconv mblen mbrlen memchr memset nl_langinfo strdup])dnl

gl_INIT
AC_CHECK_FUNCS([snprintf vasprintf strnlen wcslen wcsnlen mbrtowc wcrtomb])
dnl# Use the _snprintf function only if it is declared (because on NetBSD it
dnl# is defined as a weak alias of snprintf; we prefer to use the latter).
AC_CHECK_DECLS([_snprintf],[],[],[#include <stdio.h>])
gt_PRINTF_POSIX

dnl# Check for tools needed for formatting the documentation.
ac_aux_dir_abs=`cd ${ac_aux_dir} && pwd`
AC_PATH_PROG([DVIPS],[dvips],[${ac_aux_dir_abs}/missing dvips])
AC_PATH_PROG([TEXI2PDF],[texi2pdf],[${ac_aux_dir_abs}/missing texi2pdf])
AC_PATH_PROG([PERL],[perl],[${ac_aux_dir_abs}/missing perl])dnl

# Output.
AC_CONFIG_FILES([Makefile])dnl

AC_OUTPUT
