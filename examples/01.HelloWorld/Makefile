# Makefile for Irrlicht Examples
# It's usually sufficient to change just the target name and source file list
# and be sure that CXX is set to a valid compiler

# Name of the executable created (.exe will be added automatically if necessary)
Target := 01.HelloWorld
# List of source files, separated by spaces
Sources := main.cpp
# Path to Irrlicht directory, should contain include/ and lib/
IrrlichtHome := ../..
# Path for the executable. Note that Irrlicht.dll should usually also be there for win32 systems
BinPath = ../../bin/$(SYSTEM)

# general compiler settings (might need to be set when compiling the lib, too)
# preprocessor flags, e.g. defines and include paths
USERCPPFLAGS = 
# compiler flags such as optimization flags
USERCXXFLAGS = -O3 -ffast-math
#USERCXXFLAGS = -g -Wall
# linker flags such as additional libraries and link paths
USERLDFLAGS =

####
#no changes necessary below this line
####

CPPFLAGS = -I$(IrrlichtHome)/include -I/usr/X11R6/include $(USERCPPFLAGS)
CXXFLAGS = $(USERCXXFLAGS) -std=c++11
LDFLAGS = $(USERLDFLAGS)

#default target is Linux
all: all_osx

# target specific settings
all_linux all_osx: LDFLAGS += -L$(IrrlichtHome)/lib/$(SYSTEM) -lIrrlicht -L/opt/local/lib/
all_linux: LDFLAGS += -L/usr/X11R6/lib$(LIBSELECT) -lGL -lXxf86vm -lXext -lX11 -lXcursor
all_linux clean_linux: SYSTEM=Linux
all_osx: SYSTEM=MacOSX
all_osx: LDFLAGS += -lSDL -framework opengl
# all_osx: LDFLAGS += -framework cocoa -framework carbon -framework IOKit

# name of the binary - only valid for targets which set SYSTEM
DESTPATH = $(BinPath)/$(Target)$(SUF)

all_linux all_osx:
	$(warning Building...)
	$(CXX) $(CPPFLAGS) $(CXXFLAGS) $(Sources) -o $(DESTPATH) $(LDFLAGS)

clean: clean_linux
	$(warning Cleaning...)

clean_linux:
	@$(RM) $(DESTPATH)

.PHONY: all clean clean_linux

#multilib handling
ifeq ($(HOSTTYPE), x86_64)
LIBSELECT=64
endif
#solaris real-time features
ifeq ($(HOSTTYPE), sun4)
LDFLAGS += -lrt
endif

