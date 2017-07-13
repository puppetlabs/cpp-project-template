FROM alpine:3.6
LABEL author="Michael Smith \"michael.smith@puppet.com\""
LABEL description="A C++ build container"

# Uses sed to patch https://svn.boost.org/trac10/ticket/12419
RUN apk add --no-cache bash alpine-sdk cmake cppcheck doxygen boost-dev yaml-cpp-dev openssl-dev \
                       curl-dev icu-dev util-linux-dev ruby ruby-irb ruby-json py2-pip valgrind gettext && \
    sed -i -e 's/sys\/poll/poll/' /usr/include/boost/asio/detail/socket_types.hpp && \
    pip install cpp-coveralls

