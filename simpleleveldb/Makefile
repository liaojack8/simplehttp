LIBEVENT ?= /usr/local
TARGET ?= /usr/local
LIBSIMPLEHTTP ?= ../simplehttp
LIBSIMPLEHTTP_INC ?= $(LIBSIMPLEHTTP)/..
LIBSIMPLEHTTP_LIB ?= $(LIBSIMPLEHTTP)
LIBLEVELDB ?= /usr/local

CFLAGS = -I. -I$(LIBSIMPLEHTTP_INC) -I$(LIBEVENT)/include -I$(LIBLEVELDB)/include -Wall -g -O2 
LIBS = -L. -L$(LIBSIMPLEHTTP_LIB) -L$(LIBEVENT)/lib -L/usr/local/lib -L$(LIBLEVELDB)/lib -levent -ljson-c -lsimplehttp -lleveldb -lm -lstdc++ -lsnappy -lpthread
AR = ar
AR_FLAGS = rc
RANLIB = ranlib

TARGETS = simpleleveldb leveldb_to_csv csv_to_leveldb

SOURCES_simpleleveldb = simpleleveldb.c str_list_set.c
SOURCES_leveldb_to_csv = leveldb_to_csv.c
SOURCES_csv_to_leveldb = csv_to_leveldb.c

all: $(TARGETS)

-include $(TARGETS:%=%.deps)

$(TARGETS): %: %.c
	$(CC) $(CFLAGS) -MM -MT $@ -MF $@.deps $(SOURCES_$@)
	$(CC) $(CFLAGS) -o $@ $(SOURCES_$@) $(LIBS)

install:
	/usr/bin/install -d $(TARGET)/bin/
	/usr/bin/install simpleleveldb $(TARGET)/bin/
	/usr/bin/install leveldb_to_csv $(TARGET)/bin/
	/usr/bin/install csv_to_leveldb $(TARGET)/bin/

clean:
	rm -rf *.a *.o *.deps *.dSYM $(TARGETS)
