# Sample makefile for programs that use the ROSE library.
#
# ROSE has a number of configuration details that must be present when
# compiling and linking a user program with ROSE, and some of these
# details are difficult to get right.  The most foolproof way to get
# these details into your own makefile is to use the "rose-config"
# tool.
#
#
# This makefile assumes:
#   1. The ROSE library has been properly installed (refer to the
#      documentation for configuring, building, and installing ROSE).
#
#   2. The top of the installation directory is $(ROSE_HOME). This
#      is the same directory you specified for the "--prefix" argument
#      of the "configure" script, or the "CMAKE_INSTALL_PREFIX" if using
#      cmake. E.g., "/usr/local".
#
# The "rose-config" tool currently only works for ROSE configured with
# GNU auto tools (e.g., you ran "configure" when you built and
# installed ROSE). The "cmake" configuration is not currently
# supported by "rose-config" [September 2015].
##############################################################################

#If the ROSE bin directory is in your path, rose-config can be found automatically
ifndef ROSE_HOME
ROSE_HOME = $(shell rose-config prefix)
endif

include $(ROSE_HOME)/install/lib/rose-config.cfg

# Standard C++ compiler stuff (see rose-config --help)
ROSE_CXX         = $(shell $(ROSE_HOME)/install/bin/rose-config ROSE_CXX)
ROSE_CPPFLAGS    = $(shell $(ROSE_HOME)/install/bin/rose-config ROSE_CPPFLAGS)
ROSE_CXXFLAGS    = $(shell $(ROSE_HOME)/install/bin/rose-config ROSE_CXXFLAGS)
ROSE_LDFLAGS     = $(shell $(ROSE_HOME)/install/bin/rose-config ROSE_LDFLAGS)
ROSE_LIBDIRS     = $(shell $(ROSE_HOME)/install/bin/rose-config ROSE_LIBDIRS)
ROSE_RPATHS      = $(shell $(ROSE_HOME)/install/bin/rose-config ROSE_RPATHS)
ROSE_LINK_RPATHS = $(shell $(ROSE_HOME)/install/bin/rose-config ROSE_LINK_RPATHS)

LOCAL_HEADER     = -I./

MOSTLYCLEANFILES =

##############################################################################
# Assuming your source code is "demo.C" to build an executable named "demo".

all: UQ_Searching

UQ_Searching.o: UQ_Searching.C
	$(ROSE_CXX) $(ROSE_CPPFLAGS) $(ROSE_CXXFLAGS) $(LOCAL_HEADER) -o $@ -c -g $^

SearchingMethod.o: SearchingMethod.C
	$(ROSE_CXX) $(ROSE_CPPFLAGS) $(ROSE_CXXFLAGS) $(LOCAL_HEADER) -o $@ -c -g $^

PostProcessing.o: PostProcessing.C
	$(ROSE_CXX) $(ROSE_CPPFLAGS) $(ROSE_CXXFLAGS) $(LOCAL_HEADER) -o $@ -c -g $^

HelpingFuncs.o: HelpingFuncs.C
	$(ROSE_CXX) $(ROSE_CPPFLAGS) $(ROSE_CXXFLAGS) $(LOCAL_HEADER) -o $@ -c -g $^

Setter.o: Setter.C
	$(ROSE_CXX) $(ROSE_CPPFLAGS) $(ROSE_CXXFLAGS) $(LOCAL_HEADER) -o $@ -c -g $^

UQ_Searching: UQ_Searching.o SearchingMethod.o PostProcessing.o HelpingFuncs.o Setter.o
	$(ROSE_CXX) $(ROSE_CXXFLAGS) -o $@ $^ $(ROSE_LDFLAGS) $(ROSE_LINK_RPATHS) -Wl,-rpath=$(ROSE_HOME)/install/lib

MOSTLYCLEANFILES += UQ_Searching UQ_Searching.o SearchingMethod.o PostProcessing.o HelpingFuncs.o Setter.o

##############################################################################
# Standard boilerplate

.PHONY: clean
clean:
	rm -f $(MOSTLYCLEANFILES)
