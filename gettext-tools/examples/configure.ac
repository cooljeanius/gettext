dnl# Configuration for the gettext-tools/examples directory of GNU gettext
dnl# Copyright (C) 2006, 2009 Free Software Foundation, Inc.
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
AC_INIT([gettext-examples],[0.18.2])
AC_CONFIG_SRCDIR([installpaths.in])
AC_CONFIG_AUX_DIR([../../build-aux])
. ${srcdir}/../../version.sh
gl_INIT_PACKAGE([gettext-examples],[${VERSION_NUMBER}])
AM_INIT_AUTOMAKE([1.2 foreign silent-rules])
AC_CONFIG_HEADERS([config.h])
AM_MAINTAINER_MODE
AC_USE_SYSTEM_EXTENSIONS

dnl# Checks for programs.
AC_PROG_CXX
AC_PROG_CC
AM_PROG_CC_C_O
AC_PROG_CPP
AC_PROG_INSTALL
AC_PROG_LN_S
AC_PROG_MAKE_SET
AC_PROG_OBJC
AC_PROG_RANLIB

dnl# Checks for header files.
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
AC_CHECK_HEADERS([stdlib.h unistd.h])dnl

dnl# Checks for typedefs, structures, and compiler characteristics.
AC_CHECK_HEADER_STDBOOL

dnl# Checks for library functions.
AC_CHECK_FUNCS([setenv])dnl

dnl# Installation directories.
test "$docdir" != '${datarootdir}/doc/${PACKAGE}' || docdir='${datarootdir}/doc/gettext'

AM_PO_SUBDIRS

aclocaldir='${datadir}/aclocal'
AC_SUBST([aclocaldir])dnl

# Output.
AC_CONFIG_FILES([Makefile],
                [FIX_MAKEFILE_TOPDIR_DISTRIB])
AC_CONFIG_FILES([installpaths])
AC_CONFIG_FILES([po/Makefile], [AM_POSTPROCESS_PO_MAKEFILE])
AC_OUTPUT
