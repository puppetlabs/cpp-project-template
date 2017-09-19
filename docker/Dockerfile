# Build clang-tidy; this takes awhile and is memory-constrained (requires 4GB).
FROM alpine:3.6
WORKDIR /usr/src/llvm
RUN apk add --no-cache alpine-sdk cmake curl util-linux-dev ninja python zlib && \
    curl -OL https://github.com/llvm-project/llvm-project-20170507/archive/release_50.zip && \
    unzip release_50.zip && \
    cmake ./llvm-project-20170507-release_50/llvm -DLLVM_ENABLE_PROJECTS="clang;clang-tools-extra" \
          -GNinja -DCMAKE_BUILD_TYPE=MinSizeRel -DLLVM_TARGETS_TO_BUILD=X86 && \
    ninja -j4 clang-tidy clang-apply-replacements


FROM alpine:3.6
LABEL author="Michael Smith \"michael.smith@puppet.com\""
LABEL description="A C++ build container"

COPY --from=0 /usr/src/llvm/bin/clang-tidy /usr/bin
COPY --from=0 /usr/src/llvm/bin/clang-apply-replacements /usr/bin

# Uses sed to patch https://svn.boost.org/trac10/ticket/12419
RUN apk add --no-cache bash alpine-sdk cmake cppcheck doxygen boost-dev yaml-cpp-dev openssl-dev \
                       curl-dev icu-dev util-linux-dev ruby ruby-irb ruby-json valgrind gettext \
                       python2-dev py2-pip libffi-dev && \
    sed -i -e 's/sys\/poll/poll/' /usr/include/boost/asio/detail/socket_types.hpp && \
    pip install cpp-coveralls
