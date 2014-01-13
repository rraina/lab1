CC = g++
MKDEP=/usr/X11R6/bin/makedepend -Y
OS := $(shell uname)
ifeq ($(OS), Darwin)
  LIBS = -framework OpenGL -framework GLUT -lc
  CFLAGS = -g -Wall -Wno-deprecated -m32
else
  LIBS = -lGL -lGLU -lglut
  CFLAGS = -g -Wall -Wno-deprecated
endif

BINS = netic netis
HDRS = netimg.h ltga.h
SRCS = ltga.cpp
HDRS_SLN = 
SRCS_SLN = netic.cpp netis.cpp
OBJS = $(SRCS:.cpp=.o) $(SRCS_SLN:.cpp=.o)

netimg: $(BINS)

netic: netic.o netimg.h
	$(CC) $(CFLAGS) -o $@ $< $(LIBS)

netis: netis.o ltga.o $(HDRS)
	$(CC) $(CFLAGS) -o $@ $< ltga.o

%.o: %.cpp
	$(CC) $(CFLAGS) $(INCLUDES) -c $<

%.o: %.c
	$(CC) $(CFLAGS) $(INCLUDES) -c $< -o $@

.PHONY: clean
clean: 
	-rm -f -r $(OBJS) *.o *~ *core* netimg $(BINS)

depend: $(SRCS) $(SRCS_SLN) $(HDRS) $(HDRS_SLN) Makefile
	$(MKDEP) $(CFLAGS) $(SRCS) $(SRCS_SLN) $(HDRS) $(HDRS_SLN) >& /dev/null

# DO NOT DELETE

ltga.o: ltga.h
netic.o: netimg.h
netis.o: ltga.h netimg.h
