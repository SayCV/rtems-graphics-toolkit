#----------------------------------------------------------------------
# Makefile for SVGAlib demo programs.
#
# This file is a part of SVGAlib.
#----------------------------------------------------------------------

include ../Makefile.cfg

srcdir    = ..
VPATH     = $(srcdir)/demos

#----------------------------------------------------------------------
# Compiler Section (overrides Makefile.cfg)
#----------------------------------------------------------------------

CFLAGS = $(WARN) $(OPTIMIZE) -I$(srcdir)/include -I$(srcdir)/gl $(DEBUG)
ifeq (a.out, $(TARGET_FORMAT))
  CFLAGS += -DSVGA_AOUT
endif

#----------------------------------------------------------------------
# Rules Section
#----------------------------------------------------------------------

PROGS    = fun testgl speedtest mousetest vgatest scrolltest testlinear \
	   keytest testaccel accel forktest eventtest spin bg_test printftest \
	   joytest mjoytest bankspeed lineart linearspeed addmodetest \
	   svidtune linearfork vgatweak

# Determine what library (static or shared) we will be linking programs with
ifdef INSTALLSHAREDLIB
  LIBS = -lvgagl -lvga
endif
ifndef LIBS
  LIBS    = ../staticlib/libvgagl.a ../staticlib/libvga.a -lm
  LVGADEP = $(LIBS)
endif

all:	$(PROGS)

.PHONY: all clean cleanbin dep

$(PROGS): $(LVGADEP)

.c:
	$(CC) $(CFLAGS) $(LDFLAGS) -o $* $*.c $(LIBS)
	chown 0 $*
	chmod 4755 $*

rwpage: rwpage.pp
	$(PC) -Rintel rwpage.pp

testaccel: testaccel.c
	$(CC) $(CFLAGS) $(LDFLAGS) -o testaccel testaccel.c $(LIBS) -lm
	chown 0 testaccel
	chmod 4755 testaccel

accel: accel.c
	$(CC) $(CFLAGS) $(LDFLAGS) -o accel accel.c $(LIBS) -lm
	chown 0 accel
	chmod 4755 accel

clean:	cleanbin
	rm -f .depend *.o *~ *.bak

cleanbin:
	rm -f $(PROGS) rwpage

#
# No dependencies required here.
#

dep:
.depend:

