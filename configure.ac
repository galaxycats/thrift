#
# Licensed to the Apache Software Foundation (ASF) under one
# or more contributor license agreements. See the NOTICE file
# distributed with this work for additional information
# regarding copyright ownership. The ASF licenses this file
# to you under the Apache License, Version 2.0 (the
# "License"); you may not use this file except in compliance
# with the License. You may obtain a copy of the License at
#
#   http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing,
# software distributed under the License is distributed on an
# "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY
# KIND, either express or implied. See the License for the
# specific language governing permissions and limitations
# under the License.
#

AC_PREREQ(2.60)

AC_INIT([thrift], [20080411])

AC_CONFIG_AUX_DIR([.])

AM_INIT_AUTOMAKE

AC_ARG_VAR([PY_PREFIX], [Prefix for installing Python modules.
                         (Normal --prefix is ignored for Python because
                         Python has different conventions.)
                         Default = "/usr"])
AS_IF([test "x$PY_PREFIX" = x], [PY_PREFIX="/usr"])

AC_ARG_VAR([JAVA_PREFIX], [Prefix for installing the Java lib jar.
                           (Normal --prefix is ignored for Java because
                           Java has different conevntions.)
                           Default = "/usr/local/lib"])
AS_IF([test "x$JAVA_PREFIX" = x], [JAVA_PREFIX="/usr/local/lib"])

AC_PROG_CC
AC_PROG_CPP
AC_PROG_CXX
AC_PROG_INSTALL
AC_PROG_LIBTOOL
AC_PROG_MAKE_SET
AC_PROG_YACC
AC_PROG_LEX
AM_PROG_LEX
AC_PROG_LN_S
AC_PROG_MKDIR_P

AC_LANG([C++])

AX_THRIFT_LIB(cpp, [C++], yes)
have_cpp=no
if test "$with_cpp" = "yes";  then
  AX_BOOST_BASE([1.33.1])
  if test "x$succeeded" == "xyes" ; then
    have_cpp="yes"
  fi

  AX_LIB_EVENT([1.0])
  have_libevent=$success

  AX_LIB_ZLIB([1.2.3])
  have_zlib=$success
fi
AM_CONDITIONAL([WITH_CPP], [test "$have_cpp" = "yes"])
AM_CONDITIONAL([AMX_HAVE_LIBEVENT], [test "$have_libevent" = "yes"])
AM_CONDITIONAL([AMX_HAVE_ZLIB], [test "$have_zlib" = "yes"])

AX_THRIFT_LIB(csharp, [C#], yes)
if test "$with_csharp" = "yes";  then
  PKG_CHECK_MODULES(MONO, mono >= 2.0.0, net_3_5=yes, net_3_5=no)
  PKG_CHECK_MODULES(MONO, mono >= 1.2.4, have_mono=yes, have_mono=no)
fi
AM_CONDITIONAL(WITH_MONO, [test "$have_mono" = "yes"])
AM_CONDITIONAL(NET_2_0, [test "$net_3_5" = "no"])

AX_THRIFT_LIB(java, [Java], yes)
have_java=no
if test "$with_java" = "yes";  then
  AX_JAVAC_AND_JAVA
  AC_PATH_PROG([ANT], [ant])
  AX_CHECK_JAVA_CLASS(org.apache.log4j.Logger)
  have_log4j="$success"
  AX_CHECK_JAVA_CLASS(org.apache.commons.lang.builder.HashCodeBuilder)
  have_hashcode="$success"
  if test "x$have_log4j" = "xyes" && test "x$have_hashcode" = "xyes" ; then
    ANT_FLAGS="$ANT_FLAGS -Dnoivy="
  fi
  AC_SUBST(CLASSPATH)
  AC_SUBST(ANT_FLAGS)
  if test "x$JAVAC" != "x" && test "x$JAVAC" != "x" && test "x$ANT" != "x" ; then
    have_java="yes"
  fi
fi
AM_CONDITIONAL([WITH_JAVA], [test "$have_java" = "yes"])

AX_THRIFT_LIB(erlang, [Erlang], yes)
have_erlang=no
if test "$with_erlang" = "yes";  then
  AC_PATH_PROG([ERLC], [erlc])
  if test "x$ERLC" != "x" ; then
    have_erlang="yes"
  fi
fi
AM_CONDITIONAL(WITH_ERLANG, [test "$have_erlang" = "yes"])

AX_THRIFT_LIB(py, [Python], yes)
have_python=no
if test "$with_py" = "yes";  then
  AM_PATH_PYTHON(2.4,, :)
  if test "x$PYTHON" != "x" && test "x$PYTHON" != "x:" ; then
    have_python="yes"
  fi
fi
AM_CONDITIONAL(WITH_PYTHON, [test "$have_python" = "yes"])

AX_THRIFT_LIB(perl, [Perl], yes)
have_perl=no
if test "$with_perl" = "yes"; then
  AC_PATH_PROG([PERL], [perl])
  if test "x$PERL" != "x" ; then
    have_perl="yes"
  fi
fi
AM_CONDITIONAL(WITH_PERL, [test "$have_perl" = "yes"])

AX_THRIFT_LIB(ruby, [Ruby], yes)
have_ruby=no
if test "$with_ruby" = "yes"; then
  AC_PATH_PROG([RUBY], [ruby])
  AC_PATH_PROG([RSPEC], [spec])
  if test "x$RUBY" != "x" ; then
    have_ruby="yes"
  fi
fi
AM_CONDITIONAL(WITH_RUBY, [test "$have_ruby" = "yes"])
AM_CONDITIONAL(HAVE_RSPEC, [test "x$RSPEC" != "x"])


AC_C_CONST
AC_C_INLINE
AC_C_VOLATILE

AC_HEADER_STDBOOL
AC_HEADER_STDC
AC_HEADER_TIME
AC_CHECK_HEADERS([arpa/inet.h])
AC_CHECK_HEADERS([endian.h])
AC_CHECK_HEADERS([fcntl.h])
AC_CHECK_HEADERS([inttypes.h])
AC_CHECK_HEADERS([limits.h])
AC_CHECK_HEADERS([netdb.h])
AC_CHECK_HEADERS([netinet/in.h])
AC_CHECK_HEADERS([pthread.h])
AC_CHECK_HEADERS([stddef.h])
AC_CHECK_HEADERS([stdlib.h])
AC_CHECK_HEADERS([sys/socket.h])
AC_CHECK_HEADERS([sys/time.h])
AC_CHECK_HEADERS([unistd.h])
AC_CHECK_HEADERS([libintl.h])
AC_CHECK_HEADERS([malloc.h])

AC_CHECK_LIB(pthread, pthread_create)
AC_CHECK_LIB(rt, sched_get_priority_min)

AC_TYPE_INT16_T
AC_TYPE_INT32_T
AC_TYPE_INT64_T
AC_TYPE_INT8_T
AC_TYPE_MODE_T
AC_TYPE_OFF_T
AC_TYPE_SIZE_T
AC_TYPE_SSIZE_T
AC_TYPE_UINT16_T
AC_TYPE_UINT32_T
AC_TYPE_UINT64_T
AC_TYPE_UINT8_T
AC_CHECK_TYPES([ptrdiff_t], [], [exit 1])

AC_STRUCT_TM

AC_FUNC_ALLOCA
AC_FUNC_MALLOC
AC_FUNC_MEMCMP
AC_FUNC_REALLOC
AC_FUNC_SELECT_ARGTYPES
AC_FUNC_STAT
AC_FUNC_STRERROR_R
AC_FUNC_STRFTIME
AC_FUNC_VPRINTF
AC_CHECK_FUNCS([strtoul])
AC_CHECK_FUNCS([bzero])
AC_CHECK_FUNCS([clock_gettime])
AC_CHECK_FUNCS([ftruncate])
AC_CHECK_FUNCS([gethostbyname])
AC_CHECK_FUNCS([gettimeofday])
AC_CHECK_FUNCS([memmove])
AC_CHECK_FUNCS([memset])
AC_CHECK_FUNCS([mkdir])
AC_CHECK_FUNCS([realpath])
AC_CHECK_FUNCS([select])
AC_CHECK_FUNCS([socket])
AC_CHECK_FUNCS([strchr])
AC_CHECK_FUNCS([strdup])
AC_CHECK_FUNCS([strerror])
AC_CHECK_FUNCS([strstr])
AC_CHECK_FUNCS([strtol])
AC_CHECK_FUNCS([sqrt])

AX_SIGNED_RIGHT_SHIFT

AX_THRIFT_GEN(cpp, [C++], yes)
AM_CONDITIONAL([THRIFT_GEN_cpp], [test "$ax_thrift_gen_cpp" = "yes"])
AX_THRIFT_GEN(java, [Java], yes)
AM_CONDITIONAL([THRIFT_GEN_java], [test "$ax_thrift_gen_java" = "yes"])
AX_THRIFT_GEN(csharp, [C#], yes)
AM_CONDITIONAL([THRIFT_GEN_csharp], [test "$ax_thrift_gen_csharp" = "yes"])
AX_THRIFT_GEN(py, [Python], yes)
AM_CONDITIONAL([THRIFT_GEN_py], [test "$ax_thrift_gen_py" = "yes"])
AX_THRIFT_GEN(rb, [Ruby], yes)
AM_CONDITIONAL([THRIFT_GEN_rb], [test "$ax_thrift_gen_rb" = "yes"])
AX_THRIFT_GEN(perl, [Perl], yes)
AM_CONDITIONAL([THRIFT_GEN_perl], [test "$ax_thrift_gen_perl" = "yes"])
AX_THRIFT_GEN(php, [PHP], yes)
AM_CONDITIONAL([THRIFT_GEN_php], [test "$ax_thrift_gen_php" = "yes"])
AX_THRIFT_GEN(erl, [Erlang], yes)
AM_CONDITIONAL([THRIFT_GEN_erl], [test "$ax_thrift_gen_erl" = "yes"])
AX_THRIFT_GEN(cocoa, [Cocoa], yes)
AM_CONDITIONAL([THRIFT_GEN_cocoa], [test "$ax_thrift_gen_cocoa" = "yes"])
AX_THRIFT_GEN(st, [Smalltalk], yes)
AM_CONDITIONAL([THRIFT_GEN_st], [test "$ax_thrift_gen_st" = "yes"])
AX_THRIFT_GEN(ocaml, [OCaml], yes)
AM_CONDITIONAL([THRIFT_GEN_ocaml], [test "$ax_thrift_gen_ocaml" = "yes"])
AX_THRIFT_GEN(hs, [Haskell], yes)
AM_CONDITIONAL([THRIFT_GEN_hs], [test "$ax_thrift_gen_hs" = "yes"])
AX_THRIFT_GEN(xsd, [XSD], yes)
AM_CONDITIONAL([THRIFT_GEN_xsd], [test "$ax_thrift_gen_xsd" = "yes"])
AX_THRIFT_GEN(html, [HTML], yes)
AM_CONDITIONAL([THRIFT_GEN_html], [test "$ax_thrift_gen_html" = "yes"])

AC_CONFIG_HEADERS(config.h:config.hin)

AC_CONFIG_FILES([
  Makefile
  compiler/cpp/Makefile
  lib/Makefile
  lib/cpp/Makefile
  lib/cpp/test/Makefile
  lib/cpp/thrift.pc
  lib/cpp/thrift-nb.pc
  lib/cpp/thrift-z.pc
  lib/csharp/Makefile
  lib/java/Makefile
  lib/perl/Makefile
  lib/perl/test/Makefile
  lib/py/Makefile
  lib/rb/Makefile
  test/Makefile
  test/py/Makefile
  test/rb/Makefile
])

AC_OUTPUT


echo
echo "$PACKAGE $VERSION"
echo
echo "Building code generators ..... :$thrift_generators"
echo
echo "Building C++ Library ......... : $have_cpp"
echo "Building Java Library ........ : $have_java"
echo "Building C# Library .......... : $have_mono"
echo "Building Python Library ...... : $have_python"
echo "Building Ruby Library ........ : $have_ruby"
echo "Building Perl Library ........ : $have_perl"
echo "Building Erlang Library ...... : $have_erlang"
if test "$have_cpp" = "yes" ; then
  echo
  echo "Building TZlibTransport ...... : $have_zlib"
  echo "Building TNonblockingServer .. : $have_libevent"
fi
if test "$have_java" = "yes" ; then
  echo
  echo "Using javac .................. : $JAVAC"
  echo "Using java ................... : $JAVA"
  echo "Using ant .................... : $ANT"
fi
if test "$have_mono" = "yes" ; then
  echo
  echo "Using .NET 3.5 ............... : $net_3_5"
fi
if test "$have_python" = "yes" ; then
  echo
  echo "Using Python ................. : $PYTHON"
fi
if test "$have_ruby" = "yes" ; then
  echo
  echo "Using Ruby ................... : $RUBY"
  echo "Using rspec .................. : $RSPEC"
fi
if test "$have_perl" = "yes" ; then
  echo
  echo "Using Perl ................... : $PERL"
fi
if test "$have_erlang" = "yes" ; then
  echo
  echo "Using erlc ................... : $ERLC"
fi
echo
echo "If something is missing that you think should be present,"
echo "please skim the output of configure to find the missing"
echo "component.  Details are present in config.log."
