ACLOCAL_AMFLAGS = -I m4

# -----------------------------------------------------------------
#   Makefile for GCTA 
#   
#   Supported platforms
#       Unix / Linux                UNIX
#       Windows                     WIN
#       MacOS                       MAC
# ---------------------------------------------------------------------

# Set this variable to either UNIX, MAC or WIN
SYS = UNIX
OUTPUT = gcta64

# Use sinlge precision to store matrix
SINGLE_PRECISION = 

# Put C++ compiler here; Windows has it's own specific version
CXX_UNIX = @CXX@
CXX_WIN = C:\CodeBlocks\MinGW\bin\mingw32-g++.exe
CXX_MAC = @CXX@

# Put the path of library EIGEN here
# Library EIGEN (version 3.0.3) is freely available at http://eigen.tuxfamily.org/
EigenLib = ./eigen

# Any other compiler flags here ( -Wall, -g, etc)
CPPFLAGS = @CPPFLAGS@
CXXFLAGS = @CXXFLAGS@
CXXFLAGS += -w -O3 -I $(EigenLib) -DEIGEN_NO_DEBUG -msse2 -I.
LDFLAGS = @LDFLAGS@

ifdef SINGLE_PRECISION
 CXXFLAGS += -DSINGLE_PRECISION=1
endif

LIB = @LIB@

# Some system specific flags

ifeq ($(SYS),WIN)
 CXXFLAGS += -DWIN -static -I ../../Lib/zlib
 LIB += ../../Lib/zlib/zlib.lib
 CXX = $(CXX_WIN)
endif

ifeq ($(SYS),UNIX)
 CXXFLAGS += -DUNIX -static
 LIB += -lz
 CXX = $(CXX_UNIX)
endif

ifeq ($(SYS),MAC)
 CXXFLAGS += -DUNIX -Dfopen64=fopen #-isysroot /Developer/SDKs/MacOSX10.5.sdk -mmacosx-version-min=10.5
 LIB += -lz
 CXX = $(CXX_MAC)
endif

ifeq ($(SYS),SOLARIS)
 CXX = $(CXX_UNIX)
endif

HDR = @HDR@

HDR += CommFunc.h \
	   cdflib.h \
	   dcdflib.h \
           gcta.h \
	   ipmpar.h \
           StatFunc.h \
           StrFunc.h \
           zfstream.h
SRC = CommFunc.cpp \
           data.cpp \
	   dcdflib.cpp \
           est_hsq.cpp \
           grm.cpp \
           gwas_simu.cpp \
           ld.cpp \
           option.cpp \
           raw_geno.cpp \
           StatFunc.cpp \
           StrFunc.cpp \
           zfstream.cpp

OBJ = $(SRC:.cpp=.o)

all : $(OUTPUT) 

$(OUTPUT) :
	$(CXX) $(CPPFLAGS) $(CXXFLAGS) -o $(OUTPUT) $(OBJ) $(LDFLAGS) $(LIB) 

$(OBJ) : $(HDR)

.cpp.o : 
	$(CXX) $(CPPFLAGS) $(CXXFLAGS) -c $*.cpp

SUFFIXES : .cpp .c .o $(SUFFIXES)

$(OUTPUT) : $(OBJ)

FORCE:

clean:
	@RM@ -f *.o *~
