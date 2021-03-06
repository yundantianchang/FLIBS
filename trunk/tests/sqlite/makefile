# Makefile for "fsqlite" library
#
# NOTE:
# The source code uses the C-Fortran interface features of Fortran 2003.
# This takes care of the naming and calling conventions.
#
# $Id: makefile,v 1.1 2008/05/04 13:23:56 arjenmarkus Exp $
#
include ../../config/config.mk
include ../../config/options.mk

PROGRAMS	=	test_sqlite$(EXEEXT) \
           csvdata$(EXEEXT) \

LIBRARIES	=	libfsqlite$(LIBEXT) \

#
# Use the correct macro for interfacing between Fortran and C and
# add the directory where the Sqlite3 header file can be found
#
#DEFINES	=	-DDBL_UNDERSCORE -I../../../sqlite
#DEFINES	=	-DLOWERCASE -I../../../sqlite
#DEFINES	=	-I../../../sqlite


all:	$(PROGRAMS) $(LIBRARIES)

csvdata$(EXEEXT):	csvdata.f90
	$(FC) $(LDOUTPUT) csvdata.f90

test_sqlite$(EXEEXT):	csvtable$(OBJEXT) libfsqlite$(LIBEXT)
	$(LD) $(LDFLAGS) $(LDOUTPUT) csvtable$(OBJEXT) libfsqlite$(LIBEXT) $(EXTRALIBS)

csvtable$(OBJEXT):	csvtable.f90 fsqlite$(OBJEXT)
	$(FC) $(FFLAGS) csvtable.f90

libfsqlite$(LIBEXT):	fsqlite$(OBJEXT) csqlite$(OBJEXT) sqlite3$(OBJEXT)
	$(MKLIB) $(LIBOUT)libfsqlite$(LIBEXT) fsqlite$(OBJEXT) csqlite$(OBJEXT) sqlite3$(OBJEXT)

fsqlite$(OBJEXT):	../../src/sqlite/fsqlite.f90
	$(FC) $(FFLAGS) ../../src/sqlite/fsqlite.f90

csqlite$(OBJEXT):	../../src/sqlite/csqlite.c
	$(CC) $(CFLAGS) ../../src/sqlite/csqlite.c $(DEFINES)

sqlite3$(OBJEXT):	../../src/sqlite/sqlite3.c ../../src/sqlite/sqlite3.h
	$(CC) $(CFLAGS) ../../src/sqlite/sqlite3.c $(DEFINES)

clean:	
	$(DELETE) *$(OBJEXT)
	$(DELETE) $(PROGRAMS)
	$(DELETE) *$(MODEXT)
	$(DELETE) *$(LIBEXT)

