CFLAGS += -I../..

CPPFLAGS += -I../..

LDFLAGS += -L../../framework -lmlt -lm

include ../../../config.mak

include config.mak

TARGET = ../libmltsox$(LIBSUF)

OBJS = factory.o \
	   filter_sox.o 

SRCS := $(OBJS:.o=.c)

all: 	$(TARGET)

$(TARGET): $(OBJS)
		$(CC) $(SHFLAGS) -o $@ $(OBJS) $(LDFLAGS)

depend:	$(SRCS)
		$(CC) -MM $(CPPFLAGS) $^ 1>.depend

distclean:	clean
		rm -f .depend

clean:	
		rm -f $(OBJS) $(TARGET)

install: all
	install -m 755 $(TARGET) "$(DESTDIR)$(moduledir)"
	install -d "$(DESTDIR)$(mltdatadir)/sox"
	install -m 644 filter_sox.yml "$(DESTDIR)$(mltdatadir)/sox"
	install -m 644 filter_sox_effect.yml "$(DESTDIR)$(mltdatadir)/sox"

uninstall:
	rm "$(DESTDIR)$(moduledir)/libmltsox$(LIBSUF)" 2> /dev/null || true
	rm -rf "$(DESTDIR)$(mltdatadir)/sox"

ifneq ($(wildcard .depend),)
include .depend
endif
