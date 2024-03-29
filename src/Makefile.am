ACLOCAL_AMFLAGS = -I m4
AM_CPPFLAGS     =

AM_CPPFLAGS += -I"@HASHPIPE_INCDIR@"
AM_CPPFLAGS += -I"@XGPU_INCDIR@"

# AM_CFLAGS is used for all C compiles
AM_CFLAGS = -ggdb -fPIC -O3 -Wall -Werror -fno-strict-aliasing -mavx

# Convenience variables to group source files
paper_databuf = paper_databuf.h \
	        paper_databuf.c

paper_threads = paper_fake_net_thread.c       \
		paper_gpu_cpu_output_thread.c \
		paper_gpu_output_thread.c     \
		paper_gpu_thread.c            \
		paper_fluff_thread.c          \
		paper_net_thread.c            \
		paper_crc_thread.c

paper_fluff = paper_fluff.h \
	      paper_fluff.c

# This is the paper_gpu plugin itself
lib_LTLIBRARIES = paper_gpu.la
paper_gpu_la_SOURCES  = $(paper_databuf) $(paper_threads) $(paper_fluff)
paper_gpu_la_LIBADD   = -lrt -lxgpu
paper_gpu_la_LDFLAGS  = -avoid-version -module -shared -export-dynamic
paper_gpu_la_LDFLAGS += -L"@XGPU_LIBDIR@" -Wl,-rpath,"@XGPU_LIBDIR@"
paper_gpu_la_LDFLAGS += -L"@HASHPIPE_LIBDIR@" -Wl,-rpath,"@HASHPIPE_LIBDIR@"

# Installed scripts
dist_bin_SCRIPTS = paper_init.sh \
		   paper_crc_init.sh \
		   xtor_down.sh \
		   xtor_up.sh

# Non-installed test programs
noinst_PROGRAMS = paper_fluff_test
paper_fluff_test_SOURCES = paper_fluff_test.c $(paper_fluff)
# The paper_fluff_test_CFLAGS is an autotools workaround.
# http://www.gnu.org/software/automake/manual/html_node/Objects-created-both-with-libtool-and-without.html
paper_fluff_test_CFLAGS = $(AM_CFLAGS)
paper_fluff_test_LDADD = -lrt

# vi: set ts=8 noet :
