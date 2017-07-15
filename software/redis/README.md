版本 4.0.0(redis-4.0.0.tar.gz)


# install
https://redis.io/download


```bash
wget http://download.redis.io/releases/redis-4.0.0.tar.gz
tar xzf redis-4.0.0.tar.gz
cd redis-4.0.0
make
cd src
./redis-server
```


输出
```bash
me@mypc:~$ wget http://download.redis.io/releases/redis-4.0.0.tar.gz
--2017-07-15 16:59:06--  http://download.redis.io/releases/redis-4.0.0.tar.gz
Resolving download.redis.io (download.redis.io)... 109.74.203.151
Connecting to download.redis.io (download.redis.io)|109.74.203.151|:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 1710169 (1.6M) [application/x-gzip]
Saving to: ‘redis-4.0.0.tar.gz’

redis-4.0.0.tar.gz                   100%[===================================================================>]   1.63M   426KB/s    in 3.9s    

2017-07-15 16:59:12 (426 KB/s) - ‘redis-4.0.0.tar.gz’ saved [1710169/1710169]

me@mypc:~$ tar xzf redis-4.0.0.tar.gz
me@mypc:~$ cd redis-4.0.0
me@mypc:~/redis-4.0.0$ make
cd src && make all
make[1]: Entering directory '/home/me/redis-4.0.0/src'
    CC Makefile.dep
rm -rf redis-server redis-sentinel redis-cli redis-benchmark redis-check-rdb redis-check-aof *.o *.gcda *.gcno *.gcov redis.info lcov-html Makefile.dep dict-benchmark
(cd ../deps && make distclean)
make[2]: Entering directory '/home/me/redis-4.0.0/deps'
(cd hiredis && make clean) > /dev/null || true
(cd linenoise && make clean) > /dev/null || true
(cd lua && make clean) > /dev/null || true
(cd jemalloc && [ -f Makefile ] && make distclean) > /dev/null || true
(rm -f .make-*)
make[2]: Leaving directory '/home/me/redis-4.0.0/deps'
(rm -f .make-*)
echo STD=-std=c99 -pedantic -DREDIS_STATIC='' >> .make-settings
echo WARN=-Wall -W -Wno-missing-field-initializers >> .make-settings
echo OPT=-O2 >> .make-settings
echo MALLOC=jemalloc >> .make-settings
echo CFLAGS= >> .make-settings
echo LDFLAGS= >> .make-settings
echo REDIS_CFLAGS= >> .make-settings
echo REDIS_LDFLAGS= >> .make-settings
echo PREV_FINAL_CFLAGS=-std=c99 -pedantic -DREDIS_STATIC='' -Wall -W -Wno-missing-field-initializers -O2 -g -ggdb   -I../deps/hiredis -I../deps/linenoise -I../deps/lua/src -DUSE_JEMALLOC -I../deps/jemalloc/include >> .make-settings
echo PREV_FINAL_LDFLAGS=  -g -ggdb -rdynamic >> .make-settings
(cd ../deps && make hiredis linenoise lua jemalloc)
make[2]: Entering directory '/home/me/redis-4.0.0/deps'
(cd hiredis && make clean) > /dev/null || true
(cd linenoise && make clean) > /dev/null || true
(cd lua && make clean) > /dev/null || true
(cd jemalloc && [ -f Makefile ] && make distclean) > /dev/null || true
(rm -f .make-*)
(echo "" > .make-cflags)
(echo "" > .make-ldflags)
MAKE hiredis
cd hiredis && make static
make[3]: Entering directory '/home/me/redis-4.0.0/deps/hiredis'
cc -std=c99 -pedantic -c -O3 -fPIC  -Wall -W -Wstrict-prototypes -Wwrite-strings -g -ggdb  net.c
cc -std=c99 -pedantic -c -O3 -fPIC  -Wall -W -Wstrict-prototypes -Wwrite-strings -g -ggdb  hiredis.c
cc -std=c99 -pedantic -c -O3 -fPIC  -Wall -W -Wstrict-prototypes -Wwrite-strings -g -ggdb  sds.c
cc -std=c99 -pedantic -c -O3 -fPIC  -Wall -W -Wstrict-prototypes -Wwrite-strings -g -ggdb  async.c
cc -std=c99 -pedantic -c -O3 -fPIC  -Wall -W -Wstrict-prototypes -Wwrite-strings -g -ggdb  read.c
ar rcs libhiredis.a net.o hiredis.o sds.o async.o read.o
make[3]: Leaving directory '/home/me/redis-4.0.0/deps/hiredis'
MAKE linenoise
cd linenoise && make
make[3]: Entering directory '/home/me/redis-4.0.0/deps/linenoise'
cc  -Wall -Os -g  -c linenoise.c
make[3]: Leaving directory '/home/me/redis-4.0.0/deps/linenoise'
MAKE lua
cd lua/src && make all CFLAGS="-O2 -Wall -DLUA_ANSI -DENABLE_CJSON_GLOBAL -DREDIS_STATIC='' " MYLDFLAGS="" AR="ar rcu"
make[3]: Entering directory '/home/me/redis-4.0.0/deps/lua/src'
cc -O2 -Wall -DLUA_ANSI -DENABLE_CJSON_GLOBAL -DREDIS_STATIC=''    -c -o lapi.o lapi.c
cc -O2 -Wall -DLUA_ANSI -DENABLE_CJSON_GLOBAL -DREDIS_STATIC=''    -c -o lcode.o lcode.c
cc -O2 -Wall -DLUA_ANSI -DENABLE_CJSON_GLOBAL -DREDIS_STATIC=''    -c -o ldebug.o ldebug.c
cc -O2 -Wall -DLUA_ANSI -DENABLE_CJSON_GLOBAL -DREDIS_STATIC=''    -c -o ldo.o ldo.c
ldo.c: In function ‘f_parser’:
ldo.c:496:7: warning: unused variable ‘c’ [-Wunused-variable]
   int c = luaZ_lookahead(p->z);
       ^
cc -O2 -Wall -DLUA_ANSI -DENABLE_CJSON_GLOBAL -DREDIS_STATIC=''    -c -o ldump.o ldump.c
cc -O2 -Wall -DLUA_ANSI -DENABLE_CJSON_GLOBAL -DREDIS_STATIC=''    -c -o lfunc.o lfunc.c
cc -O2 -Wall -DLUA_ANSI -DENABLE_CJSON_GLOBAL -DREDIS_STATIC=''    -c -o lgc.o lgc.c
cc -O2 -Wall -DLUA_ANSI -DENABLE_CJSON_GLOBAL -DREDIS_STATIC=''    -c -o llex.o llex.c
cc -O2 -Wall -DLUA_ANSI -DENABLE_CJSON_GLOBAL -DREDIS_STATIC=''    -c -o lmem.o lmem.c
cc -O2 -Wall -DLUA_ANSI -DENABLE_CJSON_GLOBAL -DREDIS_STATIC=''    -c -o lobject.o lobject.c
cc -O2 -Wall -DLUA_ANSI -DENABLE_CJSON_GLOBAL -DREDIS_STATIC=''    -c -o lopcodes.o lopcodes.c
cc -O2 -Wall -DLUA_ANSI -DENABLE_CJSON_GLOBAL -DREDIS_STATIC=''    -c -o lparser.o lparser.c
cc -O2 -Wall -DLUA_ANSI -DENABLE_CJSON_GLOBAL -DREDIS_STATIC=''    -c -o lstate.o lstate.c
cc -O2 -Wall -DLUA_ANSI -DENABLE_CJSON_GLOBAL -DREDIS_STATIC=''    -c -o lstring.o lstring.c
cc -O2 -Wall -DLUA_ANSI -DENABLE_CJSON_GLOBAL -DREDIS_STATIC=''    -c -o ltable.o ltable.c
cc -O2 -Wall -DLUA_ANSI -DENABLE_CJSON_GLOBAL -DREDIS_STATIC=''    -c -o ltm.o ltm.c
cc -O2 -Wall -DLUA_ANSI -DENABLE_CJSON_GLOBAL -DREDIS_STATIC=''    -c -o lundump.o lundump.c
cc -O2 -Wall -DLUA_ANSI -DENABLE_CJSON_GLOBAL -DREDIS_STATIC=''    -c -o lvm.o lvm.c
cc -O2 -Wall -DLUA_ANSI -DENABLE_CJSON_GLOBAL -DREDIS_STATIC=''    -c -o lzio.o lzio.c
cc -O2 -Wall -DLUA_ANSI -DENABLE_CJSON_GLOBAL -DREDIS_STATIC=''    -c -o strbuf.o strbuf.c
cc -O2 -Wall -DLUA_ANSI -DENABLE_CJSON_GLOBAL -DREDIS_STATIC=''    -c -o fpconv.o fpconv.c
cc -O2 -Wall -DLUA_ANSI -DENABLE_CJSON_GLOBAL -DREDIS_STATIC=''    -c -o lauxlib.o lauxlib.c
cc -O2 -Wall -DLUA_ANSI -DENABLE_CJSON_GLOBAL -DREDIS_STATIC=''    -c -o lbaselib.o lbaselib.c
cc -O2 -Wall -DLUA_ANSI -DENABLE_CJSON_GLOBAL -DREDIS_STATIC=''    -c -o ldblib.o ldblib.c
cc -O2 -Wall -DLUA_ANSI -DENABLE_CJSON_GLOBAL -DREDIS_STATIC=''    -c -o liolib.o liolib.c
cc -O2 -Wall -DLUA_ANSI -DENABLE_CJSON_GLOBAL -DREDIS_STATIC=''    -c -o lmathlib.o lmathlib.c
cc -O2 -Wall -DLUA_ANSI -DENABLE_CJSON_GLOBAL -DREDIS_STATIC=''    -c -o loslib.o loslib.c
cc -O2 -Wall -DLUA_ANSI -DENABLE_CJSON_GLOBAL -DREDIS_STATIC=''    -c -o ltablib.o ltablib.c
cc -O2 -Wall -DLUA_ANSI -DENABLE_CJSON_GLOBAL -DREDIS_STATIC=''    -c -o lstrlib.o lstrlib.c
cc -O2 -Wall -DLUA_ANSI -DENABLE_CJSON_GLOBAL -DREDIS_STATIC=''    -c -o loadlib.o loadlib.c
cc -O2 -Wall -DLUA_ANSI -DENABLE_CJSON_GLOBAL -DREDIS_STATIC=''    -c -o linit.o linit.c
cc -O2 -Wall -DLUA_ANSI -DENABLE_CJSON_GLOBAL -DREDIS_STATIC=''    -c -o lua_cjson.o lua_cjson.c
cc -O2 -Wall -DLUA_ANSI -DENABLE_CJSON_GLOBAL -DREDIS_STATIC=''    -c -o lua_struct.o lua_struct.c
cc -O2 -Wall -DLUA_ANSI -DENABLE_CJSON_GLOBAL -DREDIS_STATIC=''    -c -o lua_cmsgpack.o lua_cmsgpack.c
cc -O2 -Wall -DLUA_ANSI -DENABLE_CJSON_GLOBAL -DREDIS_STATIC=''    -c -o lua_bit.o lua_bit.c
ar rcu liblua.a lapi.o lcode.o ldebug.o ldo.o ldump.o lfunc.o lgc.o llex.o lmem.o lobject.o lopcodes.o lparser.o lstate.o lstring.o ltable.o ltm.o lundump.o lvm.o lzio.o strbuf.o fpconv.o lauxlib.o lbaselib.o ldblib.o liolib.o lmathlib.o loslib.o ltablib.o lstrlib.o loadlib.o linit.o lua_cjson.o lua_struct.o lua_cmsgpack.o lua_bit.o	# DLL needs all object files
ar: `u' modifier ignored since `D' is the default (see `U')
ranlib liblua.a
cc -O2 -Wall -DLUA_ANSI -DENABLE_CJSON_GLOBAL -DREDIS_STATIC=''    -c -o lua.o lua.c
cc -o lua  lua.o liblua.a -lm 
liblua.a(loslib.o): In function `os_tmpname':
loslib.c:(.text+0x28c): warning: the use of `tmpnam' is dangerous, better use `mkstemp'
cc -O2 -Wall -DLUA_ANSI -DENABLE_CJSON_GLOBAL -DREDIS_STATIC=''    -c -o luac.o luac.c
cc -O2 -Wall -DLUA_ANSI -DENABLE_CJSON_GLOBAL -DREDIS_STATIC=''    -c -o print.o print.c
cc -o luac  luac.o print.o liblua.a -lm 
make[3]: Leaving directory '/home/me/redis-4.0.0/deps/lua/src'
MAKE jemalloc
cd jemalloc && ./configure --with-lg-quantum=3 --with-jemalloc-prefix=je_ --enable-cc-silence CFLAGS="-std=gnu99 -Wall -pipe -g3 -O3 -funroll-loops " LDFLAGS=""
checking for xsltproc... false
checking for gcc... gcc
checking whether the C compiler works... yes
checking for C compiler default output file name... a.out
checking for suffix of executables... 
checking whether we are cross compiling... no
checking for suffix of object files... o
checking whether we are using the GNU C compiler... yes
checking whether gcc accepts -g... yes
checking for gcc option to accept ISO C89... none needed
checking how to run the C preprocessor... gcc -E
checking for grep that handles long lines and -e... /bin/grep
checking for egrep... /bin/grep -E
checking for ANSI C header files... yes
checking for sys/types.h... yes
checking for sys/stat.h... yes
checking for stdlib.h... yes
checking for string.h... yes
checking for memory.h... yes
checking for strings.h... yes
checking for inttypes.h... yes
checking for stdint.h... yes
checking for unistd.h... yes
checking whether byte ordering is bigendian... no
checking size of void *... 8
checking size of int... 4
checking size of long... 8
checking size of intmax_t... 8
checking build system type... x86_64-unknown-linux-gnu
checking host system type... x86_64-unknown-linux-gnu
checking whether pause instruction is compilable... yes
checking for ar... ar
checking malloc.h usability... yes
checking malloc.h presence... yes
checking for malloc.h... yes
checking whether malloc_usable_size definition can use const argument... no
checking whether __attribute__ syntax is compilable... yes
checking whether compiler supports -fvisibility=hidden... yes
checking whether compiler supports -Werror... yes
checking whether tls_model attribute is compilable... yes
checking whether compiler supports -Werror... yes
checking whether alloc_size attribute is compilable... yes
checking whether compiler supports -Werror... yes
checking whether format(gnu_printf, ...) attribute is compilable... yes
checking whether compiler supports -Werror... yes
checking whether format(printf, ...) attribute is compilable... yes
checking for a BSD-compatible install... /usr/bin/install -c
checking for ranlib... ranlib
checking for ld... /usr/bin/ld
checking for autoconf... false
checking for memalign... yes
checking for valloc... yes
checking configured backtracing method... N/A
checking for sbrk... yes
checking whether utrace(2) is compilable... no
checking whether valgrind is compilable... no
checking whether a program using __builtin_ffsl is compilable... yes
checking LG_PAGE... 12
checking pthread.h usability... yes
checking pthread.h presence... yes
checking for pthread.h... yes
checking for pthread_create in -lpthread... yes
checking for library containing clock_gettime... none required
checking for secure_getenv... yes
checking for issetugid... no
checking for _malloc_thread_cleanup... no
checking for _pthread_mutex_init_calloc_cb... no
checking for TLS... yes
checking whether C11 atomics is compilable... no
checking whether atomic(9) is compilable... no
checking whether Darwin OSAtomic*() is compilable... no
checking whether madvise(2) is compilable... yes
checking whether to force 32-bit __sync_{add,sub}_and_fetch()... no
checking whether to force 64-bit __sync_{add,sub}_and_fetch()... no
checking for __builtin_clz... yes
checking whether Darwin OSSpin*() is compilable... no
checking whether glibc malloc hook is compilable... yes
checking whether glibc memalign hook is compilable... yes
checking whether pthreads adaptive mutexes is compilable... yes
checking for stdbool.h that conforms to C99... yes
checking for _Bool... yes
configure: creating ./config.status
config.status: creating Makefile
config.status: creating jemalloc.pc
config.status: creating doc/html.xsl
config.status: creating doc/manpages.xsl
config.status: creating doc/jemalloc.xml
config.status: creating include/jemalloc/jemalloc_macros.h
config.status: creating include/jemalloc/jemalloc_protos.h
config.status: creating include/jemalloc/jemalloc_typedefs.h
config.status: creating include/jemalloc/internal/jemalloc_internal.h
config.status: creating test/test.sh
config.status: creating test/include/test/jemalloc_test.h
config.status: creating config.stamp
config.status: creating bin/jemalloc-config
config.status: creating bin/jemalloc.sh
config.status: creating bin/jeprof
config.status: creating include/jemalloc/jemalloc_defs.h
config.status: creating include/jemalloc/internal/jemalloc_internal_defs.h
config.status: creating test/include/test/jemalloc_test_defs.h
config.status: executing include/jemalloc/internal/private_namespace.h commands
config.status: executing include/jemalloc/internal/private_unnamespace.h commands
config.status: executing include/jemalloc/internal/public_symbols.txt commands
config.status: executing include/jemalloc/internal/public_namespace.h commands
config.status: executing include/jemalloc/internal/public_unnamespace.h commands
config.status: executing include/jemalloc/internal/size_classes.h commands
config.status: executing include/jemalloc/jemalloc_protos_jet.h commands
config.status: executing include/jemalloc/jemalloc_rename.h commands
config.status: executing include/jemalloc/jemalloc_mangle.h commands
config.status: executing include/jemalloc/jemalloc_mangle_jet.h commands
config.status: executing include/jemalloc/jemalloc.h commands
===============================================================================
jemalloc version   : 4.0.3-0-ge9192eacf8935e29fc62fddc2701f7942b1cc02c
library revision   : 2

CONFIG             : --with-lg-quantum=3 --with-jemalloc-prefix=je_ --enable-cc-silence 'CFLAGS=-std=gnu99 -Wall -pipe -g3 -O3 -funroll-loops ' LDFLAGS=
CC                 : gcc
CFLAGS             : -std=gnu99 -Wall -pipe -g3 -O3 -funroll-loops  -fvisibility=hidden
CPPFLAGS           :  -D_GNU_SOURCE -D_REENTRANT
LDFLAGS            : 
EXTRA_LDFLAGS      : 
LIBS               :  -lpthread
TESTLIBS           : 
RPATH_EXTRA        : 

XSLTPROC           : false
XSLROOT            : 

PREFIX             : /usr/local
BINDIR             : /usr/local/bin
DATADIR            : /usr/local/share
INCLUDEDIR         : /usr/local/include
LIBDIR             : /usr/local/lib
MANDIR             : /usr/local/share/man

srcroot            : 
abs_srcroot        : /home/me/redis-4.0.0/deps/jemalloc/
objroot            : 
abs_objroot        : /home/me/redis-4.0.0/deps/jemalloc/

JEMALLOC_PREFIX    : je_
JEMALLOC_PRIVATE_NAMESPACE
                   : je_
install_suffix     : 
autogen            : 0
cc-silence         : 1
debug              : 0
code-coverage      : 0
stats              : 1
prof               : 0
prof-libunwind     : 0
prof-libgcc        : 0
prof-gcc           : 0
tcache             : 1
fill               : 1
utrace             : 0
valgrind           : 0
xmalloc            : 0
munmap             : 0
lazy_lock          : 0
tls                : 1
cache-oblivious    : 1
===============================================================================
cd jemalloc && make CFLAGS="-std=gnu99 -Wall -pipe -g3 -O3 -funroll-loops " LDFLAGS="" lib/libjemalloc.a
make[3]: Entering directory '/home/me/redis-4.0.0/deps/jemalloc'
gcc -std=gnu99 -Wall -pipe -g3 -O3 -funroll-loops  -c -D_GNU_SOURCE -D_REENTRANT -Iinclude -Iinclude -o src/jemalloc.o src/jemalloc.c
gcc -std=gnu99 -Wall -pipe -g3 -O3 -funroll-loops  -c -D_GNU_SOURCE -D_REENTRANT -Iinclude -Iinclude -o src/arena.o src/arena.c
gcc -std=gnu99 -Wall -pipe -g3 -O3 -funroll-loops  -c -D_GNU_SOURCE -D_REENTRANT -Iinclude -Iinclude -o src/atomic.o src/atomic.c
gcc -std=gnu99 -Wall -pipe -g3 -O3 -funroll-loops  -c -D_GNU_SOURCE -D_REENTRANT -Iinclude -Iinclude -o src/base.o src/base.c
gcc -std=gnu99 -Wall -pipe -g3 -O3 -funroll-loops  -c -D_GNU_SOURCE -D_REENTRANT -Iinclude -Iinclude -o src/bitmap.o src/bitmap.c
gcc -std=gnu99 -Wall -pipe -g3 -O3 -funroll-loops  -c -D_GNU_SOURCE -D_REENTRANT -Iinclude -Iinclude -o src/chunk.o src/chunk.c
gcc -std=gnu99 -Wall -pipe -g3 -O3 -funroll-loops  -c -D_GNU_SOURCE -D_REENTRANT -Iinclude -Iinclude -o src/chunk_dss.o src/chunk_dss.c
gcc -std=gnu99 -Wall -pipe -g3 -O3 -funroll-loops  -c -D_GNU_SOURCE -D_REENTRANT -Iinclude -Iinclude -o src/chunk_mmap.o src/chunk_mmap.c
gcc -std=gnu99 -Wall -pipe -g3 -O3 -funroll-loops  -c -D_GNU_SOURCE -D_REENTRANT -Iinclude -Iinclude -o src/ckh.o src/ckh.c
gcc -std=gnu99 -Wall -pipe -g3 -O3 -funroll-loops  -c -D_GNU_SOURCE -D_REENTRANT -Iinclude -Iinclude -o src/ctl.o src/ctl.c
gcc -std=gnu99 -Wall -pipe -g3 -O3 -funroll-loops  -c -D_GNU_SOURCE -D_REENTRANT -Iinclude -Iinclude -o src/extent.o src/extent.c
gcc -std=gnu99 -Wall -pipe -g3 -O3 -funroll-loops  -c -D_GNU_SOURCE -D_REENTRANT -Iinclude -Iinclude -o src/hash.o src/hash.c
gcc -std=gnu99 -Wall -pipe -g3 -O3 -funroll-loops  -c -D_GNU_SOURCE -D_REENTRANT -Iinclude -Iinclude -o src/huge.o src/huge.c
gcc -std=gnu99 -Wall -pipe -g3 -O3 -funroll-loops  -c -D_GNU_SOURCE -D_REENTRANT -Iinclude -Iinclude -o src/mb.o src/mb.c
gcc -std=gnu99 -Wall -pipe -g3 -O3 -funroll-loops  -c -D_GNU_SOURCE -D_REENTRANT -Iinclude -Iinclude -o src/mutex.o src/mutex.c
gcc -std=gnu99 -Wall -pipe -g3 -O3 -funroll-loops  -c -D_GNU_SOURCE -D_REENTRANT -Iinclude -Iinclude -o src/pages.o src/pages.c
gcc -std=gnu99 -Wall -pipe -g3 -O3 -funroll-loops  -c -D_GNU_SOURCE -D_REENTRANT -Iinclude -Iinclude -o src/prof.o src/prof.c
gcc -std=gnu99 -Wall -pipe -g3 -O3 -funroll-loops  -c -D_GNU_SOURCE -D_REENTRANT -Iinclude -Iinclude -o src/quarantine.o src/quarantine.c
gcc -std=gnu99 -Wall -pipe -g3 -O3 -funroll-loops  -c -D_GNU_SOURCE -D_REENTRANT -Iinclude -Iinclude -o src/rtree.o src/rtree.c
gcc -std=gnu99 -Wall -pipe -g3 -O3 -funroll-loops  -c -D_GNU_SOURCE -D_REENTRANT -Iinclude -Iinclude -o src/stats.o src/stats.c
gcc -std=gnu99 -Wall -pipe -g3 -O3 -funroll-loops  -c -D_GNU_SOURCE -D_REENTRANT -Iinclude -Iinclude -o src/tcache.o src/tcache.c
gcc -std=gnu99 -Wall -pipe -g3 -O3 -funroll-loops  -c -D_GNU_SOURCE -D_REENTRANT -Iinclude -Iinclude -o src/util.o src/util.c
gcc -std=gnu99 -Wall -pipe -g3 -O3 -funroll-loops  -c -D_GNU_SOURCE -D_REENTRANT -Iinclude -Iinclude -o src/tsd.o src/tsd.c
ar crus lib/libjemalloc.a src/jemalloc.o src/arena.o src/atomic.o src/base.o src/bitmap.o src/chunk.o src/chunk_dss.o src/chunk_mmap.o src/ckh.o src/ctl.o src/extent.o src/hash.o src/huge.o src/mb.o src/mutex.o src/pages.o src/prof.o src/quarantine.o src/rtree.o src/stats.o src/tcache.o src/util.o src/tsd.o
ar: `u' modifier ignored since `D' is the default (see `U')
make[3]: Leaving directory '/home/me/redis-4.0.0/deps/jemalloc'
make[2]: Leaving directory '/home/me/redis-4.0.0/deps'
    CC adlist.o
    CC quicklist.o
    CC ae.o
    CC anet.o
    CC dict.o
    CC server.o
    CC sds.o
    CC zmalloc.o
    CC lzf_c.o
    CC lzf_d.o
    CC pqsort.o
    CC zipmap.o
    CC sha1.o
    CC ziplist.o
    CC release.o
    CC networking.o
    CC util.o
    CC object.o
    CC db.o
    CC replication.o
    CC rdb.o
    CC t_string.o
    CC t_list.o
    CC t_set.o
    CC t_zset.o
    CC t_hash.o
    CC config.o
    CC aof.o
    CC pubsub.o
    CC multi.o
    CC debug.o
    CC sort.o
    CC intset.o
    CC syncio.o
    CC cluster.o
    CC crc16.o
    CC endianconv.o
    CC slowlog.o
    CC scripting.o
    CC bio.o
    CC rio.o
    CC rand.o
    CC memtest.o
    CC crc64.o
    CC bitops.o
    CC sentinel.o
    CC notify.o
    CC setproctitle.o
    CC blocked.o
    CC hyperloglog.o
    CC latency.o
    CC sparkline.o
    CC redis-check-rdb.o
    CC redis-check-aof.o
    CC geo.o
    CC lazyfree.o
    CC module.o
    CC evict.o
    CC expire.o
    CC geohash.o
    CC geohash_helper.o
    CC childinfo.o
    CC defrag.o
    CC siphash.o
    CC rax.o
    LINK redis-server
    INSTALL redis-sentinel
    CC redis-cli.o
    LINK redis-cli
    CC redis-benchmark.o
    LINK redis-benchmark
    INSTALL redis-check-rdb
    INSTALL redis-check-aof

Hint: It's a good idea to run 'make test' ;)

make[1]: Leaving directory '/home/me/redis-4.0.0/src'
me@mypc:~/redis-4.0.0$ cd src
me@mypc:~/redis-4.0.0/src$ ./redis-server
7033:C 15 Jul 17:01:37.869 # oO0OoO0OoO0Oo Redis is starting oO0OoO0OoO0Oo
7033:C 15 Jul 17:01:37.869 # Redis version=4.0.0, bits=64, commit=00000000, modified=0, pid=7033, just started
7033:C 15 Jul 17:01:37.869 # Warning: no config file specified, using the default config. In order to specify a config file use ./redis-server /path/to/redis.conf
7033:M 15 Jul 17:01:37.870 * Increased maximum number of open files to 10032 (it was originally set to 1024).
                _._                                                  
           _.-``__ ''-._                                             
      _.-``    `.  `_.  ''-._           Redis 4.0.0 (00000000/0) 64 bit
  .-`` .-```.  ```\/    _.,_ ''-._                                   
 (    '      ,       .-`  | `,    )     Running in standalone mode
 |`-._`-...-` __...-.``-._|'` _.-'|     Port: 6379
 |    `-._   `._    /     _.-'    |     PID: 7033
  `-._    `-._  `-./  _.-'    _.-'                                   
 |`-._`-._    `-.__.-'    _.-'_.-'|                                  
 |    `-._`-._        _.-'_.-'    |           http://redis.io        
  `-._    `-._`-.__.-'_.-'    _.-'                                   
 |`-._`-._    `-.__.-'    _.-'_.-'|                                  
 |    `-._`-._        _.-'_.-'    |                                  
  `-._    `-._`-.__.-'_.-'    _.-'                                   
      `-._    `-.__.-'    _.-'                                       
          `-._        _.-'                                           
              `-.__.-'                                               

7033:M 15 Jul 17:01:37.872 # WARNING: The TCP backlog setting of 511 cannot be enforced because /proc/sys/net/core/somaxconn is set to the lower value of 128.
7033:M 15 Jul 17:01:37.872 # Server initialized
7033:M 15 Jul 17:01:37.872 # WARNING overcommit_memory is set to 0! Background save may fail under low memory condition. To fix this issue add 'vm.overcommit_memory = 1' to /etc/sysctl.conf and then reboot or run the command 'sysctl vm.overcommit_memory=1' for this to take effect.
7033:M 15 Jul 17:01:37.872 # WARNING you have Transparent Huge Pages (THP) support enabled in your kernel. This will create latency and memory usage issues with Redis. To fix this issue run the command 'echo never > /sys/kernel/mm/transparent_hugepage/enabled' as root, and add it to your /etc/rc.local in order to retain the setting after a reboot. Redis must be restarted after THP is disabled.
7033:M 15 Jul 17:01:37.872 * Ready to accept connections
```


启动客户端
```bash
me@mypc:~$ cd redis-4.0.0/
me@mypc:~/redis-4.0.0$ cd src
me@mypc:~/redis-4.0.0/src$ ./redis-cli
127.0.0.1:6379> set hello:world "hello world"
OK
127.0.0.1:6379> get hello:world
"hello world"
127.0.0.1:6379> 
```


# Reference
- https://redis.io/
- https://github.com/antirez/redis
- https://redis.io/documentation
- http://github.com/antirez/redis-doc - 文档源地址
- https://redis.io/commands
