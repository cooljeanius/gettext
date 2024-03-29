dnl Configuration for the gettext-tools directory of GNU gettext
dnl Copyright (C) 1995-1999, 2000-2011 Free Software Foundation, Inc.
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
AC_INIT([gettext-tools],[0.18.2],[ueno@gnu.org],[gettext-tools],
        [https://www.gnu.org/software/gettext/])
AC_CONFIG_SRCDIR([src/msgfmt.c])
AC_CONFIG_AUX_DIR([../build-aux])
. ${srcdir}/../version.sh
gl_INIT_PACKAGE([gettext-tools],[${VERSION_NUMBER}])
AM_INIT_AUTOMAKE([1.5 gnu no-dependencies silent-rules subdir-objects])
AC_CONFIG_HEADERS([config.h])
AC_CONFIG_MACRO_DIR([m4])
AM_MAINTAINER_MODE
AC_USE_SYSTEM_EXTENSIONS

dnl Installation directories.
test "$docdir" != '${datarootdir}/doc/${PACKAGE}' || docdir='${datarootdir}/doc/gettext'

dnl Checks for programs.
AM_PROG_AR
AC_PROG_CXX
AC_PROG_YACC
AC_PROG_CC
AM_PROG_CC_C_O
AC_PROG_CPP
AC_PROG_EGREP
AC_PROG_FGREP
AC_PROG_GCC_TRADITIONAL
AC_PROG_INSTALL
AC_PROG_RANLIB
AC_PROG_MKDIR_P

gt_JAVA_CHOICE

gt_GCJ
if test -n "$HAVE_GCJ" && test "$JAVA_CHOICE" = yes; then
  BUILDJAVAEXE=yes
else
  BUILDJAVAEXE=no
fi
AC_SUBST([BUILDJAVAEXE])

gt_JAVAEXEC
gt_JAVACOMP([1.3])
AC_CHECK_PROG([JAR], [jar], [jar])
if test -n "$HAVE_JAVACOMP" && test -n "$JAR" && test "$JAVA_CHOICE" != no; then
  BUILDJAVA=yes
else
  BUILDJAVA=no
fi
AC_SUBST([BUILDJAVA])
if test -n "$HAVE_JAVAEXEC" && test $BUILDJAVA = yes; then
  TESTJAVA=yes
else
  TESTJAVA=no
fi
AC_SUBST([TESTJAVA])

gt_CSHARPCOMP
if test -n "$HAVE_CSHARPCOMP" && test "$CSHARP_CHOICE" != no; then
  BUILDCSHARP=yes
else
  BUILDCSHARP=no
fi
AC_SUBST([BUILDCSHARP])

gt_CSHARPEXEC([csharpexec-test.exe], [$srcdir/m4])
if test -n "$HAVE_CSHARPEXEC" && test $BUILDCSHARP = yes; then
  TESTCSHARP=yes
else
  TESTCSHARP=no
fi
AC_SUBST([TESTCSHARP])

dnl Check for host type.
AC_CANONICAL_HOST

dnl Checks for compiler output filename suffixes.
AC_OBJEXT
AC_EXEEXT

dnl Make sure we see all GNU and Solaris extensions.
gl_EARLY
grgl_EARLY
gtpo_EARLY

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

dnl On Cygwin 1.7.10-1 or later, error_* variables are defined in the
dnl Cygwin DLL.  To avoid any conflict with gettext DLLs, always link
dnl to gnulib's error.c.  See GETTEXTLIB_EXPORTS_FLAGS setting below.
case "$host_os" in
  cygwin*) ac_cv_lib_error_at_line=no ;;
esac

dnl Checks for libraries.
dnl FIXME: Replace `main' with a function in `-lc':
AC_CHECK_LIB([c], [main])
dnl FIXME: Replace `main' with a function in `-liconv':
AC_CHECK_LIB([iconv], [main])
dnl FIXME: Replace `main' with a function in `-lpthread':
AC_CHECK_LIB([pthread], [main])

dnl These are the only lines required to internationalize the package.
dnl (OK, not quite, the AC_CONFIG_FILES has also some parts.)
AM_GNU_GETTEXT([use-libtool], [need-ngettext])

dnl This line internationalizes the bison generated parsers.
BISON_I18N

dnl Test whether msgmerge must be linked against libm. This is the case on
dnl most systems; but BeOS has all <math.h> functions in libc and doesn't have
dnl a libm.
MSGMERGE_LIBM=?
AC_LINK_IFELSE([AC_LANG_PROGRAM([[
   #ifndef __NO_MATH_INLINES
   # define __NO_MATH_INLINES 1 /* for glibc */
   #endif
   #include <math.h>
   double x;]], [[x = ceil(x); x = sqrt(x);]])],[MSGMERGE_LIBM=],[])
if test "$MSGMERGE_LIBM" = "?"; then
  save_LIBS="$LIBS" 
  LIBS="$LIBS -lm"
  AC_LINK_IFELSE([AC_LANG_PROGRAM([[
     #ifndef __NO_MATH_INLINES
     # define __NO_MATH_INLINES 1 /* for glibc */
     #endif
     #include <math.h>
     double x;]], [[x = ceil(x); x = sqrt(x);]])],[MSGMERGE_LIBM="-lm"],[])
  LIBS="$save_LIBS"
fi
if test "$MSGMERGE_LIBM" = "?"; then
  MSGMERGE_LIBM=
fi
AC_SUBST([MSGMERGE_LIBM])

dnl# Checks for header files, functions and declarations.
gl_INIT
grgl_INIT
gtpo_INIT

dnl# Checks for header files.
AC_FUNC_ALLOCA
AC_HEADER_RESOLV
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
AC_CHECK_HEADERS([OS.h arpa/inet.h fcntl.h float.h inttypes.h langinfo.h libintl.h limits.h locale.h malloc.h netdb.h netinet/in.h paths.h stddef.h stdint.h stdio.h stdlib.h string.h strings.h sys/acl.h sys/param.h sys/socket.h sys/time.h sys/timeb.h unistd.h utime.h wchar.h wctype.h])
AC_CHECK_HEADERS([pwd.h])dnl

dnl# Checks for typedefs, structures, and compiler characteristics.
AC_C_INLINE
AC_TYPE_UNSIGNED_LONG_LONG_INT
AC_TYPE_SIZE_T
AC_CHECK_TYPES([ptrdiff_t])
AC_TYPE_SSIZE_T
gt_TYPE_SSIZE_T
AC_TYPE_PID_T
AC_CHECK_HEADER_STDBOOL
AC_TYPE_UID_T
AC_TYPE_INT8_T
AC_TYPE_INT16_T
AC_TYPE_INT32_T
AC_TYPE_INT64_T
AC_TYPE_MODE_T
AC_FUNC_OBSTACK
AC_TYPE_OFF_T
AC_C_RESTRICT
AC_CHECK_DECLS([sys_siglist])
AC_CHECK_MEMBERS([struct stat.st_rdev])
AC_TYPE_UINT8_T
AC_TYPE_UINT16_T
AC_TYPE_UINT32_T
AC_TYPE_UINT64_T
gl_GLIBC21
if test $GLIBC21 = yes; then
  AC_CHECK_MEMBERS([struct __locale_struct.__names], , , [#include <xlocale.h>])
fi

dnl Checks for library functions.
AC_FUNC_CHOWN
AC_FUNC_ERROR_AT_LINE
AC_FUNC_FORK
AC_FUNC_FSEEKO
AC_FUNC_LSTAT_FOLLOWS_SLASHED_SYMLINK
AC_FUNC_MALLOC
AC_FUNC_MBRTOWC
AC_FUNC_MMAP
AC_FUNC_REALLOC
AC_FUNC_STRERROR_R
AC_FUNC_STRNLEN
AC_FUNC_STRTOD
AC_CHECK_FUNCS([acl alarm atexit btowc dup2 getcwd getdelim gethostbyname gethostname getpagesize gettimeofday inet_ntoa isascii iswprint localeconv mblen mbrlen memchr memmove memset mkdir nl_langinfo pathconf pow putenv re_comp regcomp rmdir select setenv setlocale socket sqrt stpcpy strcasecmp strchr strcspn strdup strerror strncasecmp strpbrk strrchr strspn strstr strtol strtoul tzset uname utime wcwidth])
AC_FUNC_FORK
gt_SIGINFO
gt_SETLOCALE

AC_C_BIGENDIAN([endianness=1], [endianness=0],
  [echo "AC-C-BIGENDIAN fails to work on your system." | sed -e 's,-,_,g' 1>&2
   echo "Please report this as a bug to bug-autoconf@gnu.org" 1>&2
   exit 1],
  [endianness=universal])
if test $endianness != universal; then
  AC_DEFINE_UNQUOTED([ENDIANNESS], [$endianness],
    [Define according to the byte order of the target machine: 1 for big endian, 0 for little endian.])
fi
dnl For possibly universal binaries, it's not possible to determine the
dnl endianness at configure time. So determine it at compile time.
AH_BOTTOM([
#ifndef ENDIANNESS
# if defined __BIG_ENDIAN__
#  define ENDIANNESS 1
# endif
# if defined __LITTLE_ENDIAN__
#  define ENDIANNESS 0
# endif
#endif
])

gt_PREREQ_HOSTNAME

dnl Compilation on mingw and Cygwin needs special Makefile rules, because
dnl 1. when we install a shared library, we must arrange to export
dnl    auxiliary pointer variables for every exported variable,
dnl 2. when we install a shared library and a static library simultaneously,
dnl    the include file specifies __declspec(dllimport) and therefore we
dnl    must arrange to define the auxiliary pointer variables for the
dnl    exported variables _also_ in the static library.
if test "$enable_shared" = yes; then
  case "$host_os" in
    mingw* | cygwin*) is_woe32dll=yes ;;
    *) is_woe32dll=no ;;
  esac
else
  is_woe32dll=no
fi
AM_CONDITIONAL([WOE32DLL], [test $is_woe32dll = yes])
if test $is_woe32dll = yes; then
  AC_DEFINE([WOE32DLL], [1],
    [Define when --enable-shared is used on mingw or Cygwin.])
fi

GETTEXTLIB_EXPORTS_FLAGS=
dnl woe32dll/gettextlib-exports.c needs to know whether the getopt facility
dnl is replaced by gnulib. GETOPT_H is set by gl_FUNC_GETOPT_POSIX, inside
dnl gl_INIT.
if test -n "$GETOPT_H"; then
  GETTEXTLIB_EXPORTS_FLAGS="-DGNULIB_DEFINED_GETOPT $GETTEXTLIB_EXPORTS_FLAGS"
fi
dnl woe32dll/gettextlib-exports.c needs to know whether the error
dnl facility is replaced by gnulib. ac_cv_lib_error_at_line is set by
dnl gl_ERROR, inside gl_INIT.
if test "$ac_cv_lib_error_at_line" = no; then
  GETTEXTLIB_EXPORTS_FLAGS="-DGNULIB_DEFINED_ERROR $GETTEXTLIB_EXPORTS_FLAGS"
fi
AC_SUBST([GETTEXTLIB_EXPORTS_FLAGS])

dnl Tell the source files that the error facility is replaced by
dnl gnulib, to make sure to prepend "rpl_" prefix to the error_*
dnl symbols.
if test "$ac_cv_lib_error_at_line" = no; then
  AC_DEFINE([GNULIB_REPLACE_ERROR], [1],
    [Define when the error facility is replaced by gnulib.])
fi

dnl Put some default definitions into config.h.
AH_TOP([
/* Default value for alignment of strings in .mo file.  */
#define DEFAULT_OUTPUT_ALIGNMENT 1
])
AH_BOTTOM([
/* A file name cannot consist of any character possible.  INVALID_PATH_CHAR
   contains the characters not allowed.  */
#if defined _MSC_VER || defined __MINGW32__
/* Woe32.  This string is valid for Windows NT/2000.  On Windows 95/98/ME some
   few characters in the range 0x80..0xff are invalid as well, but this doesn't
   matter much for our purposes.  */
# define INVALID_PATH_CHAR "\001\002\003\004\005\006\007\010\011\012\013\014\015\016\017\020\021\022\023\024\025\026\027\030\031\032\033\034\035\036\037\"*/:<>?\\|"
#elif defined MSDOS
/* Something like this for MSDOG.  */
# define INVALID_PATH_CHAR "\001\002\003\004\005\006\007\010\011\012\013\014\015\016\017\020\021\022\023\024\025\026\027\030\031\032\033\034\035\036\037 \177\\:."
#else
/* Unix.  */
# define INVALID_PATH_CHAR "\001\002\003\004\005\006\007\010\011\012\013\014\015\016\017\020\021\022\023\024\025\026\027\030\031\032\033\034\035\036\037 \177/"
#endif

/* This is the page width for the message_print function.  It should
   not be set to more than 79 characters (Emacs users will appreciate
   it).  It is used to wrap the msgid and msgstr strings, and also to
   wrap the file position (#:) comments.  */
#define PAGE_WIDTH 79

/* On Windows, variables that may be in a DLL must be marked specially.  */
#if ((defined _MSC_VER && defined _DLL) || defined WOE32DLL) && !defined IN_RELOCWRAPPER
# define DLL_VARIABLE __declspec (dllimport)
#else
# define DLL_VARIABLE
#endif

/* Extra OS/2 (emx+gcc) defines.  */
#ifdef __EMX__
# include "intl/os2compat.h"
#endif
])

dnl Check for the expat XML parser.
dnl On operating systems where binary distribution vendors are likely to
dnl ship both gettext and expat, we use dynamic loading to avoid a hard
dnl dependency from gettext to expat.
case "$host_os" in
  linux*)
    AC_DEFINE([DYNLOAD_LIBEXPAT], [1],
      [Define to 1 if libexpat shall be dynamically loaded via dlopen().])
    LIBEXPAT="-ldl"
    LTLIBEXPAT="-ldl"
    AC_SUBST([LIBEXPAT])
    AC_SUBST([LTLIBEXPAT])
    ;;
  *)
    AC_LIB_HAVE_LINKFLAGS([expat], [],
      [#include <expat.h>], [XML_ExpatVersion();])
    ;;
esac

dnl Check for nm output filter that yields the exported symbols.
gt_GLOBAL_SYMBOL_PIPE

dnl Check for Emacs and where to install .elc files.
dnl Sometimes Emacs is badly installed. Allow the user to work around it.
AC_ARG_WITH([emacs],
  [  --without-emacs         do not use Emacs, don't install po-mode],
  [gt_use_emacs=$withval],
  [gt_use_emacs=yes])
if test "$EMACS" != no; then
  AC_MSG_CHECKING([whether Emacs support is requested])
  AC_MSG_RESULT([$gt_use_emacs])
  if test "$gt_use_emacs" = no; then
    EMACS=no
  fi
fi
dnl If $EMACS = no, we won't install any Emacs Lisp (*.el) files,
dnl therefore it's useless to determine $(lispdir).
if test "$EMACS" != no; then
  AM_PATH_LISPDIR
fi

aclocaldir='${datadir}/aclocal'
AC_SUBST([aclocaldir])

dnl Check how to install the set of previous versions, for autopoint.
AC_ARG_WITH([git],
  [  --without-git           don't use git to compress the infrastructure archive],
  [gt_use_git=$withval],
  [gt_use_git=maybe])
AC_ARG_WITH([cvs],
  [  --with-cvs              use cvs to compress the infrastructure archive
                          (deprecated)],
  [gt_use_cvs=$withval],
  [gt_use_cvs=no])
AC_ARG_WITH([bzip2],
  [  --without-bzip2         don't use bzip2 to compress the infrastructure archive],
  [gt_use_bzip2=$withval],
  [gt_use_bzip2=maybe])
AC_ARG_WITH([xz],
  [  --without-xz            don't use xz to compress the infrastructure archive],
  [gt_use_xz=$withval],
  [gt_use_xz=maybe])
# The CVS format is deprecated, because "cvs init" does not work in all
# circumstances
# (see <http://lists.gnu.org/archive/html/bug-cvs/2010-05/msg00003.html>)
# and we are not allowed to distribute the cvs infrastructure files ourselves
# (see <http://lists.gnu.org/archive/html/bug-cvs/2010-06/msg00011.html>).
#
# With the archive from version 0.18.1, we can observe the following
# compression rates:
#    Size           File
#  16916480   archive.dir.tar
#   3528757   archive.dir.tar.gz
#   2621440   archive.cvs.tar
#   2082492   archive.dir.tar.bz2
#    696320   archive.git.tar
#    599046   archive.git.tar.bz2
#    592989   archive.git.tar.gz
#    588124   archive.git.tar.xz
#    457190   archive.cvs.tar.gz
#    335808   archive.cvs.tar.bz2
#    308880   archive.dir.tar.xz
#    299124   archive.cvs.tar.xz
# Among these:
#   - We don't offer the uncompressed ones, because at least gzip can be
#     assumed to be present everywhere.
#   - Among archive.git.tar.*, all have approximately the same size, because
#     git already compresses most of its repository data. Offer only .gz here.
#   - Among archive.cvs.tar.*, offer only .gz, for simplicity, since --with-cvs
#     is deprecated.
# The remaining ones are:
#    Size           File            ARCHIVE_FORMAT
#   3528757   archive.dir.tar.gz      dirgz
#   2082492   archive.dir.tar.bz2     dirbz2
#    592989   archive.git.tar.gz      git
#    457190   archive.cvs.tar.gz      cvs
#    308880   archive.dir.tar.xz      dirxz
if test "$gt_use_xz" != no && test "$gt_use_xz" != maybe; then
  # --with-xz is specified. Even if --with-git or --with-cvs or --with-bzip2 is
  # also specified, we use the dirxz format.
  ARCHIVE_FORMAT=dirxz
else
  if test "$gt_use_git" != no && test "$gt_use_git" != maybe; then
    # --with-git is specified. Even if --with-cvs or --with-bzip2 is also
    # specified, we use the git format.
    ARCHIVE_FORMAT=git
  else
    if test "$gt_use_cvs" != no; then
      # --with-cvs is specified. Even if --with-bzip2 is also specified, we use
      # the cvs format.
      ARCHIVE_FORMAT=cvs
    else
      if test "$gt_use_bzip2" != no && test "$gt_use_bzip2" != maybe; then
        # --with-bzip2 is specified. We use the dirbz2 format.
        ARCHIVE_FORMAT=dirbz2
      else
        # Neither --with-git nor --with-cvs nor --with-bzip2 nor --with-xz is
        # specified. Determine which programs are present.
        if test "$gt_use_xz" != no \
           && (xz --version) >/dev/null 2>&1 \
           && xz --version | grep lzma >/dev/null; then
          # --without-xz is not specified, and the xz program exists.
          ARCHIVE_FORMAT=dirxz
        else
          # --without-xz is specified, or the xz program is missing.
changequote(,)dnl
          if test "$gt_use_git" != no \
             && (git --version) >/dev/null 2>&1 \
             && { case `git --version | sed -e 's/^[^0-9]*//'` in
                    0.* | 1.[0-5].*) false ;;
                    *) true ;;
                  esac
                }; then
changequote([,])dnl
            # --without-git is not specified, and the git program exists
            # in version 1.6 or newer. Use git format.
            ARCHIVE_FORMAT=git
          else
            # --without-git is specified, or the git program is missing.
changequote(,)dnl
            if test "$gt_use_bzip2" != no \
               && (: | bzip2 --version) >/dev/null 2>&1 \
               && { sed_bzip2_version1='s/ \([0-9][0-9.]*\).*/ \1/'
                    sed_bzip2_version2='s/^.* //'
                    case `(: | bzip2 --version) 2>&1 \
                          | sed -e 1q \
                          | sed -e "$sed_bzip2_version1" -e "$sed_bzip2_version2"` in
                      0.*) false ;;
                      *) true ;;
                    esac
                  }; then
changequote([,])dnl
              # --without-bzip2 is not specified, and the bzip2 program exists
              # in version 1.0 or newer. Use dirbz2 format.
              ARCHIVE_FORMAT=dirbz2
            else
              # --without-bzip2 is specified, or the bzip2 program is missing.
              ARCHIVE_FORMAT=dirgz
            fi
          fi
        fi
      fi
    fi
  fi
fi
AC_SUBST([ARCHIVE_FORMAT])

dnl Check for tools needed for formatting the documentation.
ac_aux_dir_abs=`cd $ac_aux_dir && pwd`
AC_PATH_PROG([DVIPS], [dvips], [$ac_aux_dir_abs/missing dvips])
AC_PATH_PROG([TEXI2PDF], [texi2pdf], [$ac_aux_dir_abs/missing texi2pdf])
AC_PATH_PROG([PERL], [perl], [$ac_aux_dir_abs/missing perl])

dnl Check for tools needed for formatting man pages.
CROSS_COMPILING=$cross_compiling
AC_SUBST([CROSS_COMPILING])

dnl Checks for optional programs for the tests/lang-*, tests/recode-* tests.
gl_PROG_ANSI_CXX([CXX], [ANSICXX])
gt_LOCALE_FR
gt_LOCALE_FR_UTF8
gt_LOCALE_JA

dnl Checks for functions for the tests/*.c tests.
AC_CHECK_FUNCS_ONCE([getrlimit setrlimit uselocale])

dnl Prepares the libtool configuration for languages used by the tests.
LT_LANG([C++])

dnl Check whether to execute tests that rely on libasprintf.
dnl This test must be consistent with gettext-runtime/configure.ac.
if test "${enable_libasprintf+set}" = set; then
  if test "$enable_libasprintf" != no; then
    TESTLIBASPRINTF=yes
  else
    TESTLIBASPRINTF=no
  fi
else
  TESTLIBASPRINTF=yes
fi
if test "$CXX" = no; then
  TESTLIBASPRINTF=no
fi
AC_SUBST([TESTLIBASPRINTF])

dnl Generate the version information file in the intl/ directory.
test -d intl || mkdir intl
echo "GNU gettext library from gettext-$VERSION" > intl/VERSION
cat > intl/ChangeLog.inst <<EOF
$RELEASE_DATE  GNU  <bug-gnu-gettext@gnu.org>

	* Version $VERSION released.

EOF

AC_CONFIG_SUBDIRS([examples])

AC_CONFIG_FILES([Makefile])

AC_CONFIG_FILES([doc/Makefile])

AC_CONFIG_FILES([intl/Makefile:../gettext-runtime/intl/Makefile.in], [
  # Change srcdir variable so that it points to ../gettext-runtime/intl.
  sed -e 's|^srcdir =.*$|srcdir = $(top_srcdir)/../gettext-runtime/intl|' \
      -e 's|^VPATH =.*$||' \
    < intl/Makefile > intl/Makefile.tmp
  mv intl/Makefile.tmp intl/Makefile
  ])

AC_CONFIG_FILES([gnulib-lib/Makefile])

AC_CONFIG_FILES([libgrep/Makefile])

AC_CONFIG_FILES([src/Makefile])
AC_CONFIG_FILES([src/user-email:src/user-email.sh.in])

AC_CONFIG_FILES([libgettextpo/Makefile])
AC_CONFIG_FILES([libgettextpo/exported.sh])

AC_CONFIG_FILES([po/Makefile.in])

AC_CONFIG_FILES([projects/Makefile])

AC_CONFIG_FILES([styles/Makefile])

AC_CONFIG_FILES([misc/Makefile])
AC_CONFIG_FILES([misc/gettextize], [chmod a+x misc/gettextize])
AC_CONFIG_FILES([misc/autopoint], [chmod a+x misc/autopoint])
AC_CONFIG_FILES([misc/convert-archive], [chmod a+x misc/convert-archive])

AC_CONFIG_FILES([man/Makefile],
                [FIX_MAKEFILE_DISTRIB])
AC_CONFIG_FILES([man/x-to-1])

AC_CONFIG_FILES([m4/Makefile])

AC_CONFIG_FILES([tests/Makefile])

AC_CONFIG_FILES([gnulib-tests/Makefile])

AC_OUTPUT
