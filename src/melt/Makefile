include ../../config.mak

OBJS = melt.o \
	   io.o

CFLAGS += -I.. $(RDYNAMIC) -DVERSION=\"$(version)\"

CPPFLAGS += -I..

LDFLAGS += -L../framework -lmlt -lpthread

SRCS := $(OBJS:.o=.c)

ifeq ($(targetos), MinGW)
ifeq (, $(findstring MELT_NOSDL, $(CFLAGS)))
CFLAGS += $(shell sdl-config --cflags)
LDFLAGS += $(shell sdl-config --libs)
endif
bindir = $(prefix)
endif

all: $(meltname)

$(meltname): $(OBJS)
		$(CC) -o $@ $(OBJS) $(LDFLAGS)

depend:	$(SRCS)
		$(CC) -MM $(CPPFLAGS) $^ 1>.depend

distclean:	clean
		rm -f .depend

clean:	
		rm -f $(OBJS) $(meltname)

install:	all
	install -d "$(DESTDIR)$(bindir)"
	install -c -m 755 $(meltname) "$(DESTDIR)$(bindir)"
ifeq ($(extra_versioning), true)
ifeq ($(melt_noversion), false)
	ln -s $(meltname) "$(DESTDIR)$(bindir)/melt"
endif
endif

uninstall:
	rm -f "$(DESTDIR)$(bindir)/$(meltname)"
ifeq ($(extra_versioning), true)
ifeq ($(melt_noversion), false)
	rm -f "$(DESTDIR)$(bindir)/melt"
endif
endif

ifneq ($(wildcard .depend),)
include .depend
endif
