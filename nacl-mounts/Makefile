#ARCH=$1 BIT=$2
NACL=$(NACL_PREFIX)/../bin/$(ARCH)-nacl
CC=$(NACL)-gcc
CFLAGS=-m$(BIT) -c -fPIC -I$(NACL_SDK_ROOT)/$(NACL_PEPPER)/include -I$(NACL_PREFIX)/include
LDFLAGS=-lpthread -shared -Wl,-soname -Wl,libnaclmounts.so -I$(NACL_SDK_ROOT)/include

OBJS=MountManager.o KernelProxy.o PathHandle.o MainThreadRunner.o Entry.o MemMount.o MemNode.o AppEngineUrlLoader.o AppEngineMount.o AppEngineNode.o

all: shared

shared: libnaclmounts.so

libnaclmounts.so: $(OBJS)
	$(CC) $(LDFLAGS) -o libnaclmounts.so $(OBJS)

install-headers:
	mkdir $(NACL_PREFIX)/include/naclmounts
	mkdir $(NACL_PREFIX)/include/naclmounts/AppEngine
	cp AppEngine/*.h $(NACL_PREFIX)/include/naclmounts/AppEngine
	mkdir $(NACL_PREFIX)/include/naclmounts/base
	cp base/*.h $(NACL_PREFIX)/include/naclmounts/base
	mkdir $(NACL_PREFIX)/include/naclmounts/memory

MountManager.o: base/MountManager.cc
	$(CC) $(CFLAGS) $< -o $@
KernelProxy.o: base/KernelProxy.cc
	$(CC) $(CFLAGS) $< -o $@
PathHandle.o: base/PathHandle.cc
	$(CC) $(CFLAGS) $< -o $@
MainThreadRunner.o: base/MainThreadRunner.cc
	$(CC) $(CFLAGS) $< -o $@
Entry.o: base/Entry.cc
	$(CC) $(CFLAGS) $< -o $@
MemMount.o: memory/MemMount.cc
	$(CC) $(CFLAGS) $< -o $@
MemNode.o: memory/MemNode.cc
	$(CC) $(CFLAGS) $< -o $@
AppEngineUrlLoader.o: AppEngine/AppEngineUrlLoader.cc
	$(CC) $(CFLAGS) $< -o $@
AppEngineMount.o: AppEngine/AppEngineMount.cc
	$(CC) $(CFLAGS) $< -o $@
AppEngineNode.o: AppEngine/AppEngineNode.cc
	$(CC) $(CFLAGS) $< -o $@

clean:
	rm -f $(OBJS) libnaclmounts.so
