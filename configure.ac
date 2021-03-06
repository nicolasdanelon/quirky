AC_INIT([Quirky IRC Client], 1, [ikey@evolve-os.com], [quirky], [https://evolve-os.com/])
AM_INIT_AUTOMAKE([-Wno-portability no-dist-gzip dist-xz foreign subdir-objects])
AC_PROG_CC
AC_PROG_CC_STDC
LT_PREREQ(2.2)
AC_CONFIG_HEADERS([config.h])
AC_PREFIX_DEFAULT(/usr/local)
AM_SILENT_RULES([yes])
LT_INIT([disable-static])

# Package requirements
PKG_CHECK_MODULES([GOBJECT], [gobject-2.0 >= 2.40.0])
PKG_CHECK_MODULES([GIO], [gio-2.0 >= 2.40.0])
PKG_CHECK_MODULES([GTK], [gtk+-3.0 >= 3.12.0])


AC_CONFIG_MACRO_DIR([m4])

AC_ARG_ENABLE(windows-build, AS_HELP_STRING([--enable-windows-build], [enable windows build @<:@default=no@:>@]),
	      [], [enable_windows_build=no])
AS_IF([test "x$enable_windows_build" = "xyes"],
	[AC_DEFINE([BUILD_WINDOWS], [1], [Building with Windows specific features])],
	[])
AM_CONDITIONAL([BUILD_WINDOWS], [test x$enable_windows_build = x"yes"])

if test "x$enable_windows_build" = "xyes"; then
    VALAFLAGS="--define WINDOWSBUILD"
fi

AC_SUBST(VALAFLAGS)

AC_PATH_PROG(GLIB_COMPILE_RESOURCES, glib-compile-resources)

# Need Vala.
AM_PROG_VALAC([0.24], [], [AC_MSG_ERROR([valac is required to build Quirky])])

AC_CONFIG_FILES([Makefile
                 data/Makefile
                 src/Makefile])
AC_OUTPUT

AC_MSG_RESULT([
        quirky $VERSION
        ========

        prefix:                 ${prefix}
        libdir:                 ${libdir}
        sysconfdir:             ${sysconfdir}
        exec_prefix:            ${exec_prefix}
        bindir:                 ${bindir}
        datarootdir:            ${datarootdir}

        compiler:               ${CC}
        cflags:                 ${CFLAGS}
        ldflags:                ${LDFLAGS}

        windows-build:          ${enable_windows_build}
])
