AC_INIT(enigma2,2.4)
AM_INIT_AUTOMAKE(enigma2,2.4)

TUXBOX_APPS
TUXBOX_APPS_DIRECTORY

AC_PROG_CC
AC_PROG_CXX
AC_PROG_RANLIB

AC_ARG_WITH(libsdl,
	AC_HELP_STRING([--with-libsdl], [use sdl, yes or no]),
	[[withsdl=$withval]],
	[[withsdl=yes]]
)

AC_CHECK_HEADER(dreamdvd/ddvdlib.h,have_ddvdlib="yes",have_ddvdlib="no")
if test x"${have_ddvdlib}" = xyes ; then
	AC_DEFINE(HAVE_DDVDLIB, 1,[Define if ddvdlib is available])
else
	AC_MSG_NOTICE([ddvdlib not found... dont build dvd plugin])
fi
AM_CONDITIONAL(HAVE_DDVDLIB, test "$have_ddvdlib" = "yes")

AM_PATH_PYTHON()
AC_PYTHON_DEVEL
#AM_PATH_XINE(1.1.0,, AC_MSG_ERROR([*** Please install xine-lib (devel) first ***]))

TUXBOX_APPS_DVB

_TUXBOX_APPS_LIB_PKGCONFIG_OPTIONAL(FREETYPE, freetype2, HAVE_FREETYPE2)
if test "$HAVE_FREETYPE2" = "no" ; then
	TUXBOX_APPS_LIB_CONFIG(FREETYPE, freetype-config)
fi
TUXBOX_APPS_LIB_PKGCONFIG(FRIBIDI,fribidi)
TUXBOX_APPS_LIB_PKGCONFIG(ID3TAG,id3tag)
TUXBOX_APPS_LIB_PKGCONFIG(MAD,mad)
#TUXBOX_APPS_LIB_PKGCONFIG(PLUGINS,tuxbox-plugins)
TUXBOX_APPS_LIB_PKGCONFIG(PNG,libpng)
TUXBOX_APPS_LIB_PKGCONFIG(SIGC,sigc++-1.2)
TUXBOX_APPS_LIB_PKGCONFIG(DVBSI,libdvbsi++)
_TUXBOX_APPS_LIB_PKGCONFIG_OPTIONAL(GSTREAMER,gstreamer,HAVE_GSTREAMER)
_TUXBOX_APPS_LIB_PKGCONFIG_OPTIONAL(GSTREAMERPBUTILS,gstreamer-pbutils,HAVE_GSTSTREAMERPBUTILS)
_TUXBOX_APPS_LIB_PKGCONFIG_OPTIONAL(LIBXINE,libxine,HAVE_LIBXINE)
AC_CHECK_LIB(jpeg, jpeg_set_defaults, HAVE_JPEG="yes", HAVE_JPEG="no")
JPEG_LIBS="-ljpeg"
AC_SUBST(JPEG_LIBS)

AC_SUBST(LIBUNGIF_LIBS,"")
AC_CHECK_HEADERS(gif_lib.h,
	AC_CHECK_LIB(ungif,DGifOpen,
	[AC_DEFINE(HAVE_LIBUNGIF,1,[Define if you have libgif/libungif including devel headers])
		LIBUNGIF_LIBS="-lungif"],
		[AC_CHECK_LIB(gif,DGifOpen,
			[AC_DEFINE(HAVE_LIUNBGIF,1)
			LIBUNGIF_LIBS="-lgif"])]))

TUXBOX_APPS_LIB_PKGCONFIG(XML2,libxml-2.0)

# ok, we are in trouble: XMLCCWRAP only defines C++ symbols. So let's just check if linking works,
# and assume everything will be ok. Then just check for the "exit" symbol, which should be always there.
AC_LANG_SAVE
AC_LANG_CPLUSPLUS
TUXBOX_APPS_LIB_SYMBOL(XMLCCWRAP, xmlccwrap, exit)
AC_LANG_RESTORE

if test "$withsdl" = "yes" ; then
	_TUXBOX_APPS_LIB_PKGCONFIG_OPTIONAL(SDL,sdl,WITH_SDL)
	if test "$WITH_SDL" = "no" ; then
		TUXBOX_APPS_LIB_CONFIG(SDL,sdl-config)
		AC_DEFINE_UNQUOTED([WITH_SDL],[$withsdl],[With SDL])
	fi
fi
# allow 'if WITH_SDL' conditionals in Makefile.am
AM_CONDITIONAL(WITH_SDL, test "$WITH_SDL" = "yes")

CPPFLAGS="$CPPFLAGS "'-I$(top_srcdir)'
CPPFLAGS="$CPPFLAGS -D_REENTRANT $PYTHON_CPPFLAGS $MD5SUM_CFLAGS $FREETYPE_CFLAGS $FRIBIDI_CFLAGS $ID3TAG_CFLAGS $MAD_CFLAGS $PLUGINS_CFLAGS $PNG_CFLAGS $SDL_CFLAGS $SIGC_CFLAGS $XMLTREE_CFLAGS $DVBSI_CFLAGS $GSTREAMER_CFLAGS $GSTREAMERPBUTILS_CFLAGS $LIBXINE_CFLAGS $LIBUNGIF_CFLAGS"
#CPPFLAGS="$CPPFLAGS -DMEMLEAK_CHECK"
CXXFLAGS="$CXXFLAGS -fno-rtti -fno-exceptions -Wall"
LDFLAGS="$LDFLAGS -pthread $PYTHON_LDFLAGS $SDL_LDFLAGS $GSTREAMER_LDFLAGS $GSTREAMERPBUTILS_LDFLAGS $LIBXINE_LDFLAGS $LIBUNGIF_LDFLAGS"
#LDFLAGS="-rdynamic $LDFLAGS"

TUXBOX_APPS_GETTEXT

AC_OUTPUT([
Makefile
data/Makefile
data/fonts/Makefile
data/countries/Makefile
data/defaults/Makefile
data/defaults/Dream/Makefile
data/defaults/Dream/hdbouquets/Makefile
data/defaults/Dream/sdbouquets/Makefile
data/extensions/Makefile
data/skin_default/Makefile
data/skin_default/menu/Makefile
data/skin_default/icons/Makefile
data/skin_default/buttons/Makefile
data/skin_default/spinner/Makefile
include/Makefile
lib/Makefile
lib/actions/Makefile
lib/base/Makefile
lib/driver/Makefile
lib/dvb/Makefile
lib/dvb/lowlevel/Makefile
lib/dvb_ci/Makefile
lib/gdi/Makefile
lib/gui/Makefile
lib/mmi/Makefile
lib/nav/Makefile
lib/python/Makefile
lib/python/Components/Makefile
lib/python/Components/Converter/Makefile
lib/python/Components/Renderer/Makefile
lib/python/Components/Sources/Makefile
lib/python/Screens/Makefile
lib/python/Plugins/Makefile
lib/python/Plugins/DemoPlugins/Makefile
lib/python/Plugins/DemoPlugins/TestPlugin/Makefile
lib/python/Plugins/Extensions/CutListEditor/Makefile
lib/python/Plugins/Extensions/CutListEditor/meta/Makefile
lib/python/Plugins/Extensions/DVDBurn/Makefile
lib/python/Plugins/Extensions/DVDBurn/meta/Makefile
lib/python/Plugins/Extensions/DVDPlayer/Makefile
lib/python/Plugins/Extensions/DVDPlayer/meta/Makefile
lib/python/Plugins/Extensions/DVDPlayer/src/Makefile
lib/python/Plugins/Extensions/GraphMultiEPG/Makefile
lib/python/Plugins/Extensions/GraphMultiEPG/meta/Makefile
lib/python/Plugins/Extensions/Makefile
lib/python/Plugins/Extensions/MediaPlayer/Makefile
lib/python/Plugins/Extensions/MediaPlayer/meta/Makefile
lib/python/Plugins/Extensions/MediaScanner/Makefile
lib/python/Plugins/Extensions/MediaScanner/meta/Makefile
lib/python/Plugins/Extensions/Modem/Makefile
lib/python/Plugins/Extensions/PicturePlayer/Makefile
lib/python/Plugins/Extensions/PicturePlayer/meta/Makefile
lib/python/Plugins/Extensions/PicturePlayer/data/Makefile
lib/python/Plugins/Extensions/SocketMMI/Makefile
lib/python/Plugins/Extensions/SocketMMI/meta/Makefile
lib/python/Plugins/Extensions/SocketMMI/src/Makefile
lib/python/Plugins/Extensions/TuxboxPlugins/Makefile
lib/python/Plugins/Extensions/TuxboxPlugins/meta/Makefile
lib/python/Plugins/SystemPlugins/CleanupWizard/Makefile
lib/python/Plugins/SystemPlugins/CleanupWizard/meta/Makefile
lib/python/Plugins/SystemPlugins/CommonInterfaceAssignment/Makefile
lib/python/Plugins/SystemPlugins/CommonInterfaceAssignment/meta/Makefile
lib/python/Plugins/SystemPlugins/CrashlogAutoSubmit/Makefile
lib/python/Plugins/SystemPlugins/CrashlogAutoSubmit/meta/Makefile
lib/python/Plugins/SystemPlugins/DefaultServicesScanner/Makefile
lib/python/Plugins/SystemPlugins/DefaultServicesScanner/meta/Makefile
lib/python/Plugins/SystemPlugins/DiseqcTester/Makefile
lib/python/Plugins/SystemPlugins/DiseqcTester/meta/Makefile
lib/python/Plugins/SystemPlugins/FrontprocessorUpgrade/Makefile
lib/python/Plugins/SystemPlugins/FrontprocessorUpgrade/meta/Makefile
lib/python/Plugins/SystemPlugins/Hotplug/Makefile
lib/python/Plugins/SystemPlugins/Hotplug/meta/Makefile
lib/python/Plugins/SystemPlugins/Makefile
lib/python/Plugins/SystemPlugins/TempFanControl/Makefile
lib/python/Plugins/SystemPlugins/NetworkWizard/Makefile
lib/python/Plugins/SystemPlugins/NetworkWizard/meta/Makefile
lib/python/Plugins/SystemPlugins/NFIFlash/Makefile
lib/python/Plugins/SystemPlugins/NFIFlash/meta/Makefile
lib/python/Plugins/SystemPlugins/PositionerSetup/Makefile
lib/python/Plugins/SystemPlugins/PositionerSetup/meta/Makefile
lib/python/Plugins/SystemPlugins/SatelliteEquipmentControl/Makefile
lib/python/Plugins/SystemPlugins/SatelliteEquipmentControl/meta/Makefile
lib/python/Plugins/SystemPlugins/Satfinder/Makefile
lib/python/Plugins/SystemPlugins/Satfinder/meta/Makefile
lib/python/Plugins/SystemPlugins/SkinSelector/Makefile
lib/python/Plugins/SystemPlugins/SkinSelector/meta/Makefile
lib/python/Plugins/SystemPlugins/SoftwareManager/Makefile
lib/python/Plugins/SystemPlugins/SoftwareManager/meta/Makefile
lib/python/Plugins/SystemPlugins/VideoEnhancement/Makefile
lib/python/Plugins/SystemPlugins/VideoEnhancement/meta/Makefile
lib/python/Plugins/SystemPlugins/VideoTune/Makefile
lib/python/Plugins/SystemPlugins/VideoTune/meta/Makefile
lib/python/Plugins/SystemPlugins/Videomode/Makefile
lib/python/Plugins/SystemPlugins/Videomode/meta/Makefile
lib/python/Plugins/SystemPlugins/WirelessLan/Makefile
lib/python/Plugins/SystemPlugins/WirelessLan/meta/Makefile
lib/python/Tools/Makefile
lib/service/Makefile
lib/components/Makefile
po/Makefile
main/Makefile
tools/Makefile
enigma2.pc
])

#lib/python/Plugins/Extensions/SimpleRSS/Makefile
#lib/python/Plugins/Extensions/FileManager/Makefile
