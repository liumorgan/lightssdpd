#copyright(C) 2013 eVideo. All rights reversed.
#author xuwf

include ../Makefile.cfg

CFLAGS += -I../src

bin_PROGRAMS = ssdp_client
bin_SOURCES = ssdp_client.c
bin_OBJECTS = $(notdir $(patsubst %.c, %.o, $(patsubst %.cpp, %.o, $(bin_SOURCES)))) 

ifeq ($(ENABLE_CONVERT_CODING), 1)
	CFLAGS += -DENABLE_CONVERT_CODING
	LDFLAGS += -luchardet -liconv
endif

all:.depend $(bin_PROGRAMS)

$(bin_PROGRAMS):$(bin_OBJECTS)
	$(CC) $(CFLAGS) -o $@ $^ -L../src -lssdp $(LDFLAGS) -lpthread

.depend:
	@$(CC) $(CFLAGS) -MM $(lib_SOURCES) $(bin_SOURCES) > $@

clean:
	$(RM) $(lib_OBJECTS) $(lib_LIBRARYS) $(bin_OBJECTS) $(bin_PROGRAMS) .depend

-include .depend
%.o:%.c
	$(CC) $(CFLAGS) -c $<
%.o:%.cpp
	$(CPP) $(CPPFLAGS) -c $<


