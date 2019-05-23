# Build a newer version of cppcheck (because it's been buggy)
FROM alpine:3.6
RUN apk add --no-cache alpine-sdk cmake util-linux-dev ninja python zlib pcre-dev && \
    wget https://github.com/danmar/cppcheck/archive/1.87.tar.gz && \
    tar xzvf 1.87.tar.gz && \
    cd cppcheck-1.87 && \
    make install -j4 DESTDIR=/dest SRCDIR=build CFGDIR=/usr/share/cppcheck/cfg HAVE_RULES=yes CXXFLAGS="-O2 -DNDEBUG"


FROM alpine:3.6
LABEL author="Michael Smith \"michael.smith@puppet.com\""
LABEL description="A C++ build container"

COPY --from=0 /dest /

# Uses sed to patch https://svn.boost.org/trac10/ticket/12419
RUN apk add --no-cache bash alpine-sdk cmake doxygen boost-dev yaml-cpp-dev openssl-dev \
                       curl-dev icu-dev util-linux-dev ruby ruby-irb ruby-json valgrind gettext \
                       python2-dev py2-pip libffi-dev && \
    sed -i -e 's/sys\/poll/poll/' /usr/include/boost/asio/detail/socket_types.hpp && \
    pip install cpp-coveralls
