FROM ghcho20/centos:0

RUN yum install -y automake make gcc gcc-c++

ARG timezone
RUN echo ZONE="\"$timezone\"" > /etc/sysconfig/clock; ln -sf /usr/share/zoneinfo/$timezone /etc/localtime

ADD https://github.com/zeromq/zeromq4-x/releases/download/v4.0.4/zeromq-4.0.4.tar.gz /tmp
RUN cd /tmp; tar xvf zeromq-4.0.4.tar.gz; \
	cd zeromq-4.0.4; ./configure; make; make install; \
	cd ..; rm -rf zeromq-4.0.4; rm -f zeromq-4.0.4.tar.gz
ADD zmq.hpp /usr/local/include

ADD https://github.com/msgpack/msgpack-c/releases/download/cpp-1.1.0/msgpack-1.1.0.tar.gz /tmp
RUN cd /tmp; tar xvf msgpack-1.1.0.tar.gz; \
	cd msgpack-1.1.0; ./configure; make; make install; \
	cd ..; rm -rf msgpack-1.1.0; rm -f msgpack-1.1.0.tar.gz

ENV LD_LIBRARY_PATH /usr/local/lib

WORKDIR /root

ENTRYPOINT ["/usr/sbin/init"]
