FROM debian:jessie-backports

RUN apt-key adv --keyserver pool.sks-keyservers.net --recv-key A278B781FE4B2BDA

RUN echo 'deb http://www.apache.org/dist/cassandra/debian 39x main' >> /etc/apt/sources.list.d/cassandra.list

ENV CASSANDRA_VERSION 3.9

RUN apt-get update \
	&& apt-get install -y curl cassandra="$CASSANDRA_VERSION" \
	&& rm -rf /var/lib/apt/lists/*

ENV CASSANDRA_CONFIG /etc/cassandra

COPY docker-entrypoint.sh /docker-entrypoint.sh
ENTRYPOINT ["/docker-entrypoint.sh"]

VOLUME ["/var/lib/cassandra", "/etc/cassandra"]

# 7000: intra-node communication
# 7001: TLS intra-node communication
# 7199: JMX
# 9042: CQL
# 9160: thrift service
EXPOSE 7000 7001 7199 9042 9160
CMD ["cassandra", "-f", "-R"]
