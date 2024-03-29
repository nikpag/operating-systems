#
# Makefile
#

CC = gcc

# CAUTION: Always use '-pthread' when compiling POSIX threads-based
# applications, instead of linking with "-lpthread" directly.
CFLAGS = -Wall -O2 -pthread
LIBS =

all: pthread-test simplesync simplesync-mutex simplesync-atomic kgarten mandel simplesync_assembly simplesync-mutex_assembly simplesync-atomic_assembly

## Pthread test
pthread-test: pthread-test.o
	$(CC) $(CFLAGS) -o pthread-test pthread-test.o $(LIBS)

pthread-test.o: pthread-test.c
	$(CC) $(CFLAGS) -c -o pthread-test.o pthread-test.c

## Simple sync (two versions)

simplesync: simplesync.o
	$(CC) $(CFLAGS) -o simplesync simplesync.o $(LIBS)

simplesync-mutex: simplesync-mutex.o
	$(CC) $(CFLAGS) -o simplesync-mutex simplesync-mutex.o $(LIBS)

simplesync-atomic: simplesync-atomic.o
	$(CC) $(CFLAGS) -o simplesync-atomic simplesync-atomic.o $(LIBS)

simplesync.o: simplesync_nosync.c
	$(CC) $(CFLAGS) -DSYNC_ATOMIC -c -o simplesync.o simplesync_nosync.c

simplesync-mutex.o: simplesync.c
	$(CC) $(CFLAGS) -DSYNC_MUTEX -c -o simplesync-mutex.o simplesync.c

simplesync-atomic.o: simplesync.c
	$(CC) $(CFLAGS) -DSYNC_ATOMIC -c -o simplesync-atomic.o simplesync.c

simplesync_assembly:
	$(CC) $(CFLAGS) -S -g -DSYNC_ATOMIC -static -o simplesync.s simplesync_nosync.c

simplesync-mutex_assembly:
	$(CC) $(CFLAGS) -S -g -DSYNC_MUTEX -static -o simplesync-mutex.s simplesync.c

simplesync-atomic_assembly:
	$(CC) $(CFLAGS) -S -g -DSYNC_ATOMIC -static -o simplesync-atomic.s simplesync.c

## Kindergarten
kgarten: kgarten.o
	$(CC) $(CFLAGS) -o kgarten kgarten.o $(LIBS)

kgarten.o: kgarten.c
	$(CC) $(CFLAGS) -c -o kgarten.o kgarten.c


## Mandel
mandel: mandel-lib.o mandel.o
	$(CC) $(CFLAGS) -o mandel mandel-lib.o mandel.o $(LIBS)

mandel-lib.o: mandel-lib.h mandel-lib.c
	$(CC) $(CFLAGS) -c -o mandel-lib.o mandel-lib.c $(LIBS)

mandel.o: mandel.c
	$(CC) $(CFLAGS) -c -o mandel.o mandel.c $(LIBS)

clean:
	rm -f *.s *.o pthread-test simplesync-{atomic,mutex} kgarten mandel
