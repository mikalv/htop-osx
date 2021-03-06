#                                               -*- Autoconf -*-
# Process this file with autoconf to produce a configure script.

AC_PREREQ(2.57)
AC_INIT([htop],[0.8.2.8],[loderunner@users.sourceforge.net])
AM_INIT_AUTOMAKE
AC_CONFIG_SRCDIR([htop.c])
AC_CONFIG_HEADER([config.h])
AC_CONFIG_MACRO_DIR([m4])

# Checks for programs.
AC_PROG_CC
AM_PROG_CC_C_O

AM_DISABLE_SHARED
AM_ENABLE_STATIC
AC_PROG_LIBTOOL

# Checks for libraries.
AC_CHECK_LIB([m], [ceil], [], [missing_libraries="$missing_libraries libm"])

if test ! -z "$missing_libraries"; then
  AC_MSG_ERROR([missing libraries: $missing_libraries])
fi

# Checks for header files.
AC_HEADER_DIRENT
AC_HEADER_STDC
AC_CHECK_HEADERS([stdlib.h string.h strings.h sys/param.h sys/time.h unistd.h curses.h],[:],[
  missing_headers="$missing_headers $ac_header"
])

if test ! -z "$missing_headers"; then
  AC_MSG_ERROR([missing headers: $missing_headers])
fi

# Checks for typedefs, structures, and compiler characteristics.
AC_HEADER_STDBOOL
AC_C_CONST
AC_TYPE_PID_T
AC_TYPE_UID_T

# Checks for library functions.
AC_FUNC_CLOSEDIR_VOID
AC_FUNC_MALLOC
AC_FUNC_REALLOC
AC_TYPE_SIGNAL
AC_FUNC_STAT
AC_CHECK_FUNCS([memmove strncasecmp strstr strdup])

save_cflags="${CFLAGS}"
CFLAGS="${CFLAGS} -std=c99"
AC_MSG_CHECKING([whether gcc -std=c99 option works])
AC_TRY_COMPILE(AC_INCLUDES_DEFAULT, [char *a; a = strdup("foo"); int i = 0; i++; // C99],
   AC_MSG_RESULT([yes]),
   AC_MSG_ERROR([htop is written in C99. A newer version of gcc is required.]))
CFLAGS="$save_cflags"

AC_ARG_ENABLE(openvz, [AC_HELP_STRING([--enable-openvz], [enable OpenVZ support])], ,enable_openvz="no")
if test "x$enable_openvz" = xyes; then
   AC_DEFINE(HAVE_OPENVZ, 1, [Define if openvz support enabled.])
fi

AC_ARG_ENABLE(vserver, [AC_HELP_STRING([--enable-vserver], [enable VServer support])], ,enable_vserver="no")
if test "x$enable_vserver" = xyes; then
    AC_DEFINE(HAVE_VSERVER, 1, [Define if vserver support enabled.])
fi

AC_ARG_ENABLE(ancient_vserver, [AC_HELP_STRING([--enable-ancient-vserver], [enable ancient VServer support (implies --enable-vserver)])], ,enable_ancient_vserver="no")
if test "x$enable_ancient_vserver" = xyes; then
    AC_DEFINE(HAVE_VSERVER, 1, [Define if vserver support enabled.])
    AC_DEFINE(HAVE_ANCIENT_VSERVER, 1, [Define if ancient vserver support enabled.])
fi

AC_ARG_ENABLE(taskstats, [AC_HELP_STRING([--enable-taskstats], [enable per-task IO Stats (taskstats kernel sup required)])], ,enable_taskstats="yes")
if test "x$enable_taskstats" = xyes; then
    AC_DEFINE(HAVE_TASKSTATS, 1, [Define if taskstats support enabled.])
fi

AC_ARG_ENABLE(unicode, [AC_HELP_STRING([--enable-unicode], [enable Unicode support])], ,enable_unicode="no")
if test "x$enable_unicode" = xyes; then
   AC_CHECK_LIB([ncursesw], [refresh], [], [missing_libraries="$missing_libraries libncursesw"])
   AC_CHECK_HEADERS([ncursesw/curses.h],[:],[missing_headers="$missing_headers $ac_header"])
else
   AC_CHECK_LIB([ncurses], [refresh], [], [missing_libraries="$missing_libraries libncurses"])
   AC_CHECK_HEADERS([curses.h],[:],[missing_headers="$missing_headers $ac_header"])
fi

AC_CONFIG_FILES([Makefile])
AC_OUTPUT
