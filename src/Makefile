#copyright(C) 2013 eVideo. All rights reversed.
#author xuwf

include ../Makefile.cfg

lib_LIBRARYS = libssdp.a
lib_SOURCES = device.c \
			  http_parser.c \
			  iterator.c \
			  lightssdpc.c \
			  list.c \
			  net.c \
			  ssdp.c \
			  ssdp_log.c \
			  ssdp_packet.c \
			  threadpool.c
lib_OBJECTS = $(notdir $(patsubst %.c, %.o, $(patsubst %.cpp, %.o, $(lib_SOURCES))))
lib_LDFLAGS = -lpthread

bin_PROGRAMS = lightssdpd
bin_SOURCES = lightssdpd.c \
			  daemonize.c
bin_OBJECTS = $(notdir $(patsubst %.c, %.o, $(patsubst %.cpp, %.o, $(bin_SOURCES)))) 

ifeq ($(ENABLE_CONVERT_CODING), 1)
	CFLAGS += -DENABLE_CONVERT_CODING
	LDFLAGS += -luchardet -liconv
endif

all:.depend $(lib_LIBRARYS) $(bin_PROGRAMS)

$(lib_LIBRARYS):$(lib_OBJECTS)
	$(AR) $@ $^

$(bin_PROGRAMS):$(bin_OBJECTS)
	$(CPP) $(CFLAGS) -o $@ $^ -L. -lssdp $(LDFLAGS) -lpthread
	$(STRIP) $@

.depend:
	@$(CC) $(CFLAGS) -MM $(lib_SOURCES) $(bin_SOURCES) > $@

clean:
	$(RM) $(lib_OBJECTS) $(lib_LIBRARYS) $(bin_OBJECTS) $(bin_PROGRAMS) .depend

install:
	@$(MKDIR) $(INSTALL_DIR)/include
	@$(MKDIR) $(INSTALL_DIR)/lib
	@$(MKDIR) $(INSTALL_DIR)/bin
	$(CP) device.h $(INSTALL_DIR)/include
	$(CP) lightssdpc.h $(INSTALL_DIR)/include
	$(CP) libssdp.a	$(INSTALL_DIR)/lib
	$(CP) lightssdpd $(INSTALL_DIR)/bin

uninstall:
	$(RM) $(INSTALL_DIR)/include/device.h
	$(RM) $(INSTALL_DIR)/include/lightssdpc.h
	$(RM) $(INSTALL_DIR)/lib/libssdp.a
	$(RM) $(INSTALL_DIR)/bin/lightssdpd

-include .depend
%.o:%.c
	$(CC) $(CFLAGS) -c $<
%.o:%.cpp
	$(CPP) $(CPPFLAGS) -c $<


