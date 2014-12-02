# Copyright 2006 The Android Open Source Project

ACLOCAL_AMFLAGS = -I m4 ${ACLOCAL_FLAGS}

# Distribution
# ------------
EXTRA_DIST = \
	NOTICE \
	android-hardware-legacy-$(HARDWARE_LEGACY_API_VERSION).pc.in

DISTCLEANFILES =

# Common/global flags
# -------------------
AM_CPPFLAGS = \
	-include config.h \
	-I$(top_srcdir)/include

AM_CFLAGS = \
	-Wall -Werror

libtool_opts = \
	-version-info $(LT_VERSION_INFO) \
	-export-dynamic \
	-rpath $(libdir)

lib_LTLIBRARIES =

# libandroid-hardware-legacy.la
# -----------------------------
lib_LTLIBRARIES += \
	libandroid-hardware-legacy-0.la

libandroid_hardware_legacy_0_la_CPPFLAGS = \
	$(AM_CPPFLAGS) \
	$(LOG_CFLAGS)
libandroid_hardware_legacy_0_la_LDFLAGS = \
	$(libtool_opts)
libandroid_hardware_legacy_0_la_LIBADD = \
	$(LOG_LIBS)
libandroid_hardware_legacy_0_la_SOURCES =

if WITH_QEMU
libandroid_hardware_legacy_0_la_CPPFLAGS += \
	-DQEMU_HARDWARE
endif

include power/Android.mk
include uevent/Android.mk
include vibrator/Android.mk
include qemu/Android.mk
include qemu_tracing/Android.mk

# legacy_audio builds it's own set of libraries that aren't linked into
# hardware_legacy
# TODO: https://github.com/laarid/laarid/issues/5
#include audio/Android.mk

# hardware_legacy HEADERS
# -----------------------
hardwarelegacyincdir = $(includedir)/android/hardware-legacy-$(HARDWARE_LEGACY_API_VERSION)/hardware_legacy
hardwarelegacyinc_HEADERS = \
	include/hardware_legacy/IMountService.h \
	include/hardware_legacy/power.h \
	include/hardware_legacy/qemu_tracing.h \
	include/hardware_legacy/uevent.h \
	include/hardware_legacy/vibrator.h

# PKG-CONFIG data files
# ---------------------
pkgconfigdir = $(libdir)/pkgconfig
pkgconfig_DATA = \
	android-hardware-legacy-$(HARDWARE_LEGACY_API_VERSION).pc

$(pkgconfig_DATA): config.status

DISTCLEANFILES += \
	$(pkgconfig_DATA)
