CC = gcc
CXX = g++

WORKLOAD_TYPE = MEDIUM_

# cflags used
CFLAGS=-O3 -march=native -D$(WORKLOAD_TYPE)
CXXFLAGS=-O3 -march=native -D$(WORKLOAD_TYPE)

# common libraries used
COMMON_LIBS=-lrt -ldl -lpthread -lm

SRC_S=src/page_mod.c src/common.c src/common_rand.c
SRC_G=src/page_gen.c src/common.c src/common_rand.c

DEPS=src/config.h

# the targets
all : bin/pagerank bin/page_gen

###############################################################################
# pagerank
###############################################################################

bin/pagerank: $(SRC_S) $(DEPS)
	$(CC) $(INCLUDES) $(CFLAGS) $(SRC_S) -o $@  $(COMMON_LIBS)

bin/page_gen: $(SRC_G) $(DEPS)
	$(CC) $(INCLUDES) $(CFLAGS) $(SRC_G) -o $@  $(COMMON_LIBS)

pagerank.manifest.sgx : pagerank.manifest bin/pagerank pages_medium.dat pages_high.dat pages_low.dat
	@echo "Building pagerank"
	./build_manifest_andsign.sh pagerank

clean:
	rm -rf bin/*
