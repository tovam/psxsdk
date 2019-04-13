# Makefile for PSX SDK library

include ../Makefile.cfg

CFLAGS += -O0

# Never remove the line below!
CFLAGS += -D__IN_LIBPSX

OBJDIR = obj
OBJS =	$(patsubst src/%.c, $(OUTDIR)/%.o, $(wildcard src/*.c)) \
		$(patsubst src/libc/%.c, $(OUTDIR)/libc/%.o, $(wildcard src/libc/*.c)) \
		$(patsubst src/runexe/%.c, $(OUTDIR)/runexe/%.o, $(wildcard src/runexe/*.c)) \
		$(patsubst src/%.s, $(OUTDIR)/%.o, $(wildcard src/*.s)) \
		$(patsubst src/runexe/%.s, $(OUTDIR)/runexe/%.o, $(wildcard src/runexe/*.s))

$(OBJDIR):
	mkdir -p $(OBJDIR)

all: libpsx.a start.o

libpsx.a: $(OBJS) | $(OBJDIR)
	$(AR) r libpsx.a $(OBJS)

$(OUTDIR)/%.o: src/%.c
	$(CC) $(CFLAGS) -c -o $@ $<

$(OUTDIR)/libc:
	mkdir -p $(OUTDIR)/libc
	
$(OUTDIR)/libc/%.o: src/libc/%.c | $(OUTDIR)/libc
	$(CC) $(CFLAGS) -c -o $@ $<
	
$(OUTDIR)/runexe:
	mkdir -p $(OUTDIR)/runexe

$(OUTDIR)/runexe/%.o: src/runexe/%.c | $(OUTDIR)/runexe
	$(CC) $(CFLAGS) -c -o $@ $<
	     
$(OUTDIR)/%.o: src/%.s
	$(CC) $(CFLAGS) -c -o $@ $<
	
$(OUTDIR)/runexe/%.o: src/runexe/%.s
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
