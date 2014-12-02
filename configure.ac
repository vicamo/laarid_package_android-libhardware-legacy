# android-hardware_legacy versioning
# -------------------------
# To make new release:
#
#   hardware_legacy_micro_version += 1
#   hardware_legacy_interface_revision += 1
#
# if any functions have been added:
#
#   hardware_legacy_micro_version += 1
#   hardware_legacy_interface_revision = 0
#
#   or
#
#   hardware_legacy_minor_version += 1
#   hardware_legacy_micro_version = 0
#   hardware_legacy_interface_revision = 0
#
# if backwards compatibility has been broken:
#
#   hardware_legacy_major_version += 1
#   hardware_legacy_minor_version = 0
#   hardware_legacy_micro_version = 0
#   hardware_legacy_interface_revision = 0
m4_define([hardware_legacy_major_version], [0])
m4_define([hardware_legacy_minor_version], [0])
m4_define([hardware_legacy_micro_version], [1])
m4_define([hardware_legacy_interface_revision], [1])
m4_define([hardware_legacy_api_version], [hardware_legacy_major_version.0])
m4_define([hardware_legacy_release_number], [hardware_legacy_major_version])
m4_define([hardware_legacy_version],
  [hardware_legacy_major_version.hardware_legacy_minor_version.hardware_legacy_micro_version])

AC_INIT([android-hardware-legacy], [hardware_legacy_version],
  [https://github.com/laarid/platform_hardware_libhardware_legacy/issues], [],
  [https://github.com/laarid/platform_hardware_libhardware_legacy])

AC_CONFIG_HEADERS([config.h])
AC_CONFIG_SRCDIR([include/hardware_legacy/power.h])
AC_CONFIG_MACRO_DIR([m4])
AC_CONFIG_AUX_DIR([build-aux])

AM_INIT_AUTOMAKE([-Wall -Werror foreign subdir-objects no-define tar-ustar])
AM_MAINTAINER_MODE([enable])
AM_SILENT_RULES([yes])

HARDWARE_LEGACY_MAJOR_VERSION=hardware_legacy_major_version
HARDWARE_LEGACY_MINOR_VERSION=hardware_legacy_minor_version
HARDWARE_LEGACY_MICRO_VERSION=hardware_legacy_micro_version
HARDWARE_LEGACY_API_VERSION=hardware_legacy_api_version
HARDWARE_LEGACY_RELEASE_NUMBER=hardware_legacy_release_number
AC_SUBST([HARDWARE_LEGACY_MAJOR_VERSION])
AC_SUBST([HARDWARE_LEGACY_MINOR_VERSION])
AC_SUBST([HARDWARE_LEGACY_MICRO_VERSION])
AC_SUBST([HARDWARE_LEGACY_API_VERSION])
AC_SUBST([HARDWARE_LEGACY_RELEASE_NUMBER])

AM_PROG_AR
AC_PROG_CC
PKG_PROG_PKG_CONFIG

# libtool versioning
# ------------------
LT_INIT

m4_define([hardware_legacy_binary_age],
  [m4_eval(100 * hardware_legacy_minor_version + hardware_legacy_micro_version)])
m4_define([lt_current],
  [m4_eval(hardware_legacy_binary_age - hardware_legacy_interface_revision)])
m4_define([lt_revision], [hardware_legacy_interface_revision])
# Whenever backward compatibility is broken, we generate libraries of different
# release number. That follows the library files of the same release are always
# compatible, and they have their lt_age equal to lt_current.
m4_define([lt_age], [lt_current])
LT_VERSION_INFO="lt_current:lt_revision:lt_age"
AC_SUBST([LT_VERSION_INFO])

LT_OUTPUT

# configure arguments
# -------------------
AC_ARG_WITH([qemu],
 [AS_HELP_STRING([--with-qemu], [use qemu hardware @<:@default=no@:>@])])
AM_CONDITIONAL([WITH_QEMU], [test x$with_qemu = xyes])

# Required libraries
# ------------------
PKG_CHECK_MODULES([LOG], [android-log-0.0])
AC_SUBST([LOG_CFLAGS])
AC_SUBST([LOG_LIBS])

AC_CONFIG_FILES([
  Makefile
  android-hardware-legacy-0.0.pc
])
AC_OUTPUT
