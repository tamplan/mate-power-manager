NULL =

AM_CPPFLAGS =							\
	-I. -I$(srcdir) 					\
	$(GLIB_CFLAGS)						\
	$(DBUS_CFLAGS)						\
	$(CAIRO_CFLAGS)						\
	$(PANEL_CFLAGS)						\
	$(LIBNOTIFY_CFLAGS)					\
	-DBINDIR=\"$(bindir)\"			 		\
	-DMATELOCALEDIR=\""$(datadir)/locale"\"			\
	-DDATADIR=\"$(datadir)\"				\
	-DPREFIX=\""$(prefix)"\" 				\
	-DSYSCONFDIR=\""$(sysconfdir)"\" 			\
	-DLIBDIR=\""$(libdir)"\" 				\
	-DVERSION="\"$(VERSION)\"" 				\
	-DGPM_ICONS_DATA=\"$(pkgdatadir)/icons\"		\
	-DBRIGHTNESS_MENU_UI_DIR=\""$(uidir)"\"			\
	-DEGG_LOG_FILE=\""~/mate-power-manager.log"\"		\
	-DEGG_VERBOSE="\"GPM_VERBOSE\""				\
	-DEGG_LOGGING="\"GPM_LOGGING\""				\
	-DEGG_CONSOLE="\"GPM_CONSOLE\""				\
	$(DISABLE_DEPRECATED)					\
	$(WARN_CFLAGS)						\
	$(NULL)

libexec_PROGRAMS=mate-brightness-applet

mate_brightness_applet_SOURCES =				\
	brightness-applet.c					\
	gpm-common.c						\
	gpm-common.h

mate_brightness_applet_LDADD =					\
	$(DBUS_LIBS)						\
	$(CAIRO_LIBS)						\
	$(PANEL_LIBS)

appletdir       = $(datadir)/mate-panel/applets
applet_in_files = org.mate.BrightnessApplet.mate-panel-applet.desktop.in
applet_DATA     = $(applet_in_files:.mate-panel-applet.desktop.in=.mate-panel-applet)

$(applet_DATA): $(applet_in_files)
	$(AM_V_GEN) $(MSGFMT) --desktop --keyword=Name --keyword=Description --template $< -d $(top_srcdir)/po -o $@

$(applet_in_files): $(applet_in_files).in
	$(AM_V_GEN) sed \
            -e "s|\@LIBEXECDIR\@|$(libexecdir)|" \
            -e "s|\@VERSION\@|$(PACKAGE_VERSION)|" \
            $< > $@

servicedir       = $(datadir)/dbus-1/services
service_in_files = org.mate.panel.applet.BrightnessAppletFactory.service.in
service_DATA     = $(service_in_files:.service.in=.service)

org.mate.panel.applet.BrightnessAppletFactory.service: $(service_in_files)
	$(AM_V_GEN)sed \
            -e "s|\@LIBEXECDIR\@|$(libexecdir)|" \
            $< > $@

uidir   = $(datadir)/mate-power-manager/ui
ui_DATA = brightness-applet-menu.xml

EXTRA_DIST = $(applet_in_files).in $(ui_DATA) $(service_in_files)

DISTCLEANFILES =						\
	$(applet_DATA) $(applet_DATA).in $(service_DATA)

-include $(top_srcdir)/git.mk
