# Binary target
TGTDIR  := bin
TARGET  ?= myTest

# Code extensions
SRCEXT  := .c
INCEXT  := .h
OBJEXT  := .o

# Code directories
SRCDIR  := src
INCDIR  := include
OBJDIR  := build

# Compiler and linker
CC      := cc
LD      := cc
CCMACRO ?=
LDFLAGS :=
CCFLAGS := -O0 -Wall -Wextra $(CCMACRO)

# Code files
INCS  = $(shell find $(INCDIR) -type f -name '*$(INCEXT)')
SRCS  = $(shell find $(SRCDIR) -type f -name '*$(SRCEXT)')
OBJS  = $(patsubst $(SRCDIR)/%$(SRCEXT),$(OBJDIR)/%$(OBJEXT),$(SRCS))

# Linking
$(TARGET): $(OBJS)
		$(LD) $(LDFLAGS) -L$(OBJDIR) -o $@ $^

# Compiling
$(OBJDIR)/%$(OBJEXT): $(SRCDIR)/%$(SRCEXT) | $(OBJDIR)
		$(CC) $(CCFLAGS) -I$(INCDIR) -c -o $@ $<

# Objects directory
$(OBJDIR):
		mkdir -p $(OBJDIR)

# Target directory
$(TGTDIR):
		mkdir -p $(TGTDIR)

# First rule
all: $(TARGET) | $(TGTDIR)
		@mv $(TARGET) $(TGTDIR)/

# Run with arguments
run:
		@./$(TGTDIR)/$(TARGET) $(ARGUMENTS)

# Clean objects and binaries
clean:
		rm -rf $(OBJDIR)
		rm -rf $(TGTDIR)

# Clean and make again
again:
		@make clean
		@make

# Diagnostic to show files
show:
		@echo "Sources: $(SRCS)"
		@echo "Includes: $(INCS)"
		@echo "Objects: $(OBJS)"

.PHONY: all run clean again show
