# Makefile for PSX SDK library

include ../Makefile.cfg

CFLAGS += -O0

# Never remove the line below!
CFLAGS += -D__IN_LIBPSX

OBJDIR = obj
OBJS =	$(patsubst src/%.c, $(OBJDIR)/%.o, $(wildcard src/*.c)) \
		$(patsubst src/libc/%.c, $(OBJDIR)/libc/%.o, $(wildcard src/libc/*.c)) \
		$(patsubst src/runexe/%.c, $(OBJDIR)/runexe/%.o, $(wildcard src/runexe/*.c)) \
		$(patsubst src/%.s, $(OBJDIR)/%.o, $(wildcard src/*.s)) \
		$(patsubst src/runexe/%.s, $(OBJDIR)/runexe/%.o, $(wildcard src/runexe/*.s))

$(OBJDIR):
	mkdir -p $(OBJDIR)

all: libpsx.a start.o

libpsx.a: $(OBJS) | $(OBJDIR)
	$(AR) r libpsx.a $(OBJS)

$(OBJDIR)/%.o: src/%.c
	$(CC) $(CFLAGS) -c -o $@ $<

$(OBJDIR)/libc:
	mkdir -p $(OBJDIR)/libc
	
$(OBJDIR)/libc/%.o: src/libc/%.c | $(OBJDIR)/libc
	$(CC) $(CFLAGS) -c -o $@ $<
	
$(OBJDIR)/runexe:
	mkdir -p $(OBJDIR)/runexe

$(OBJDIR)/runexe/%.o: src/runexe/%.c | $(OBJDIR)/runexe
	$(CC) $(CFLAGS) -c -o $@ $<
	     
$(OBJDIR)/%.o: src/%.s
	$(CC) $(CFLAGS) -c -o $@ $<
	
$(OBJDIR)/runexe/%.o: src/runexe/%.s
	$(CC) $(CFLAGS) -c -o $@ $<
	
start.o: src/start/start.s
	$(CC) $(CFLAGS) -c -o $@ $<

install: libpsx.a start.o
	cp libpsx.a $(TOOLCHAIN_PREFIX)/lib
	cp start.o $(TOOLCHAIN_PREFIX)/lib
	cp -r include/*	$(TOOLCHAIN_PREFIX)/include
	
clean:
	rm -f $(OBJS)
	rm -f libpsx.a
	rm -f start.o

distclean: clean
