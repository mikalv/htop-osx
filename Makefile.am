
ACLOCAL_AMFLAGS = -I m4

bin_PROGRAMS = htop
dist_man_MANS = htop.1
EXTRA_DIST = $(dist_man_MANS) htop.desktop htop.png \
install-sh autogen.sh missing
applicationsdir = $(datadir)/applications
applications_DATA = htop.desktop
pixmapdir = $(datadir)/pixmaps
pixmap_DATA = htop.png

htop_CFLAGS = -pedantic -Wall -std=c99 -D_XOPEN_SOURCE_EXTENDED -framework IOKit -framework CoreFoundation
htop_LDFLAGS = -framework IOKit -framework CoreFoundation
AM_CPPFLAGS = -DSYSCONFDIR=\"$(sysconfdir)\"
DEFAULT_INCLUDES = -iquote .


myhtopsources = AvailableMetersPanel.c CategoriesPanel.c CheckItem.c \
ClockMeter.c ColorsPanel.c ColumnsPanel.c CPUMeter.c CRT.c DebugMemory.c \
DisplayOptionsPanel.c FunctionBar.c Hashtable.c Header.c htop.c ListItem.c \
LoadAverageMeter.c MemoryMeter.c Meter.c MetersPanel.c Object.c Panel.c \
BatteryMeter.c Process.c ProcessList.c RichString.c ScreenManager.c Settings.c \
SignalItem.c SignalsPanel.c String.c SwapMeter.c TasksMeter.c TraceScreen.c \
UptimeMeter.c UsersTable.c Vector.c AvailableColumnsPanel.c AffinityPanel.c \
HostnameMeter.c OpenFilesScreen.c util.c smc.c CPUTemperatureMeter.c FanRPMMeter.c

myhtopheaders = AvailableColumnsPanel.h AvailableMetersPanel.h \
CategoriesPanel.h CheckItem.h ClockMeter.h ColorsPanel.h ColumnsPanel.h \
CPUMeter.h CRT.h DebugMemory.h DisplayOptionsPanel.h FunctionBar.h \
Hashtable.h Header.h htop.h ListItem.h LoadAverageMeter.h MemoryMeter.h \
BatteryMeter.h Meter.h MetersPanel.h Object.h Panel.h ProcessList.h RichString.h \
ScreenManager.h Settings.h SignalItem.h SignalsPanel.h String.h \
SwapMeter.h TasksMeter.h TraceScreen.h UptimeMeter.h UsersTable.h Vector.h \
Process.h AffinityPanel.h HostnameMeter.h OpenFilesScreen.h util.h smc.h CPUTemperatureMeter.h \
FanRPMMeter.h

SUFFIXES = .h

BUILT_SOURCES = $(myhtopheaders)
htop_SOURCES = $(myhtopheaders) $(myhtopsources) config.h debug.h

profile:
	$(MAKE) all CFLAGS="-pg -O2"

debug:
	$(MAKE) all CFLAGS="-ggdb -DDEBUG"

hardened-debug:
	$(MAKE) all CFLAGS="-ggdb -DDEBUG" LDFLAGS="-nopie"
 
debuglite:
	$(MAKE) all CFLAGS="-ggdb -DDEBUGLITE"

install-exec-hook:
	chmod 4755 $(DESTDIR)$(bindir)/htop
