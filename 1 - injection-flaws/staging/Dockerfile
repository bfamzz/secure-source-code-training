FROM gcc:10.3.0

RUN apt -qq -y update && apt -qq -y upgrade && \
    cd /usr/bin && mkdir gfortran && cd ../.. && \
    apt -qq -y install gfortran build-essential postgresql-client cmake libboost-all-dev libtcmalloc-minimal4 && \
	ln -s /usr/lib/libtcmalloc_minimal.so.4 /usr/lib/libtcmalloc_minimal.so && \
git clone https://github.com/jtv/libpqxx.git \
    --branch 7.5.2 --depth 1 \ 
    && cd libpqxx/ && mkdir build && cd build/ && cmake \
    -DCMAKE_BUILD_TYPE=Release \
    -DCMAKE_INSTALL_PREFIX=/usr/local \
    -DPQXX_DIR=/usr/local/lib \
    -DPostgreSQL_DIR=/usr/lib/x86_64-linux-gnu \
    -DPQXX_TYPE_INCLUDE_DIR=/usr/local/include/pqxx \
    -DPostgreSQL_TYPE_INCLUDE_DIR=/usr/include/postgresql \
    -DCMAKE_MODULE_PATH=/usr/src/libpqxx-r6.4/cmake .. \
    && make && make install && ldconfig /usr/local/lib && \
    cd ../.. && rm -rf libpqxx/