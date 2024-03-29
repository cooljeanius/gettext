dnl Configuration for the gettext-runtime directory of GNU gettext
dnl Copyright (C) 1995-1999, 2000-2010 Free Software Foundation, Inc.
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

AC_PREREQ([2.70])
AC_INIT([gettext-runtime],[0.18.2],[ueno@gnu.org],[gettext-runtime],
        [https://www.gnu.org/software/gettext/])
AC_CONFIG_SRCDIR([intl/dcigettext.c])
AC_CONFIG_AUX_DIR([../build-aux])
AC_CONFIG_MACRO_DIR([m4])
. ${srcdir}/../version.sh
gl_INIT_PACKAGE([gettext-runtime],[${VERSION_NUMBER}])
AM_INIT_AUTOMAKE([1.5 gnu no-dependencies silent-rules subdir-objects])
AC_CONFIG_HEADERS([config.h])
AM_MAINTAINER_MODE
AC_USE_SYSTEM_EXTENSIONS

dnl Installation directories.
test "$docdir" != '${datarootdir}/doc/${PACKAGE}' || docdir='${datarootdir}/doc/gettext'

dnl Checks for programs.
AC_PROG_CXX
AC_PROG_CC
AM_PROG_CC_C_O
AC_PROG_INSTALL
AC_PROG_MKDIR_P
AC_PROG_RANLIB
AC_PROG_YACC

gt_JAVA_CHOICE

gt_JAVACOMP([1.3], [1.1])
AC_CHECK_PROG([JAR], [jar], [jar])
if test -n "$HAVE_JAVACOMP" && test -n "$JAR" && test "$JAVA_CHOICE" != no; then
  BUILDJAVA=yes
else
  BUILDJAVA=no
fi
AC_SUBST([BUILDJAVA])

gt_CSHARPCOMP
if test -n "$HAVE_CSHARPCOMP" && test "$CSHARP_CHOICE" != no; then
  BUILDCSHARP=yes
else
  BUILDCSHARP=no
fi
AC_SUBST([BUILDCSHARP])

dnl Check for host type.
AC_CANONICAL_HOST

dnl Checks for compiler output filename suffixes.
AC_OBJEXT
AC_EXEEXT

dnl Make sure we see all GNU and Solaris extensions.
gl_EARLY

dnl Check for build configuration.

gl_WOE32_DLL

LT_INIT([win32-dll])

dnl Prepares the libtool configuration for handling of Windows resources, and
dnl sets the RC variable to a program that compiles Windows resource files.
LT_LANG([Windows Resource])

dnl On mingw and Cygwin, we can activate special Makefile rules which add
dnl version information to the shared libraries and executables.
case "$host_os" in
  mingw* | cygwin*) is_woe32=yes ;;
  *) is_woe32=no ;;
esac
AM_CONDITIONAL([WOE32], [test $is_woe32 = yes])

dnl Checks for libraries.

dnl These are the only lines required to internationalize the package.
dnl (OK, not quite, the AC_CONFIG_FILES has also some parts.)
AM_GNU_GETTEXT([use-libtool], [need-ngettext])

dnl Checks for header files, functions and declarations.
gl_INIT
AC_TYPE_SIZE_T
AC_CHECK_HEADER_STDBOOL
AC_TYPE_UID_T
AC_C_INLINE
AC_TYPE_INT32_T
AC_TYPE_MODE_T
AC_FUNC_OBSTACK
AC_TYPE_OFF_T
AC_TYPE_PID_T
AC_C_RESTRICT
AC_TYPE_SSIZE_T
AC_CHECK_MEMBERS([struct stat.st_rdev])
AC_TYPE_UINT8_T
AC_TYPE_UINT16_T
AC_TYPE_UINT32_T
AC_CHECK_TYPES([ptrdiff_t])
AC_FUNC_ALLOCA
AC_CHECK_HEADERS([OS.h argz.h fcntl.h float.h inttypes.h langinfo.h libintl.h limits.h locale.h malloc.h netdb.h stddef.h stdint.h stdio_ext.h stdlib.h string.h sys/param.h sys/time.h unistd.h wchar.h wctype.h])
AC_FUNC_ERROR_AT_LINE
AC_FUNC_LSTAT_FOLLOWS_SLASHED_SYMLINK
AC_FUNC_MALLOC
AC_FUNC_MBRTOWC
AC_FUNC_MMAP
AC_FUNC_REALLOC
AC_FUNC_STRERROR_R
AC_FUNC_STRNLEN
AC_CHECK_FUNCS([__argz_count __argz_next __argz_stringify atexit dup2 getcwd getpagesize getwd iswprint localeconv mblen mbrlen memchr memmove mempcpy memset munmap nl_langinfo pathconf setenv setlocale stpcpy strcasecmp strchr strcspn strdup strerror strrchr strstr strtol strtoul wcwidth])

dnl Put some default definitions into config.h.
AH_BOTTOM([
/* On Windows, variables that may be in a DLL must be marked specially.  */
#if (defined _MSC_VER && defined _DLL) && !defined IN_RELOCWRAPPER
# define DLL_VARIABLE __declspec (dllimport)
#else
# define DLL_VARIABLE
#endif

/* Extra OS/2 (emx+gcc) defines.  */
#ifdef __EMX__
# include "intl/os2compat.h"
#endif
])

dnl Check for tools needed for formatting the documentation.
ac_aux_dir_abs=`cd $ac_aux_dir && pwd`
AC_PATH_PROG([PERL], [perl], [$ac_aux_dir_abs/missing perl])

dnl Check for tools needed for formatting man pages.
CROSS_COMPILING=$cross_compiling
AC_SUBST([CROSS_COMPILING])

dnl Checks for optional programs for the tests/lang-* tests.
gl_PROG_ANSI_CXX([CXX], [ANSICXX])

dnl Checks for special libraries for the tests/test-lock test.
dnl On some systems, sched_yield is in librt, rather than in libpthread.
LIBSCHED=
if test $gl_threads_api = posix; then
  dnl Solaris has sched_yield in librt, not in libpthread or libc.
  AC_CHECK_LIB([rt], [sched_yield], [LIBSCHED=-lrt],
    [dnl Solaris 2.5.1, 2.6 has sched_yield in libposix4, not librt.
     AC_CHECK_LIB([posix4], [sched_yield], [LIBSCHED=-lposix4])])
fi
AC_SUBST([LIBSCHED])

dnl Determine whether to build libasprintf.
AC_ARG_ENABLE([libasprintf],
  [  --disable-libasprintf   do not build libasprintf],
  [if test "$enableval" != no; then
     SUBDIR_libasprintf=libasprintf
   else
     SUBDIR_libasprintf=
   fi
  ], [SUBDIR_libasprintf=libasprintf])
if test "$CXX" = ":"; then
  SUBDIR_libasprintf=
fi
AM_CONDITIONAL([ENABLE_LIBASPRINTF], [test -n "$SUBDIR_libasprintf"])

AC_CONFIG_SUBDIRS([libasprintf])

AC_CONFIG_FILES([Makefile])

AC_CONFIG_FILES([doc/Makefile])

AC_CONFIG_FILES([intl/Makefile])

AC_CONFIG_FILES([intl-java/Makefile])

AC_CONFIG_FILES([intl-csharp/Makefile])

AC_CONFIG_FILES([gnulib-lib/Makefile])

AC_CONFIG_FILES([src/Makefile])
AC_CONFIG_FILES([src/gettext.sh], [chmod a+x src/gettext.sh])

AC_CONFIG_FILES([po/Makefile.in])

AC_CONFIG_FILES([man/Makefile],
                [FIX_MAKEFILE_DISTRIB])
AC_CONFIG_FILES([man/x-to-1])

AC_CONFIG_FILES([m4/Makefile])

AC_CONFIG_FILES([tests/Makefile])

AC_OUTPUT
