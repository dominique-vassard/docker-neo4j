FROM neo4j:3.1
MAINTAINER <Dominique Vassard "dominique.vassard@gmail.com">

ENV APOC_VERSION 3.1.3.6
ENV APOC_JAR apoc-${APOC_VERSION}-all.jar
ENV APOC_URI https://github.com/neo4j-contrib/neo4j-apoc-procedures/releases/download/${APOC_VERSION}/apoc-${APOC_VERSION}-all.jar
 ENV NEO4J_AUTH neo4j/neo4j_pass

# Add APOC procedures plugin
RUN curl --fail --silent --show-error --location --remote-name ${APOC_URI} \
    && mv ${APOC_JAR} /var/lib/neo4j/plugins/

# Volumes definitions
VOLUME /data
VOLUME /logs
VOLUME /var/lib/neo4j/import

# Set workdir at it is in parent image
WORKDIR /var/lib/neo4j

ENTRYPOINT ["/docker-entrypoint.sh"]
CMD ["neo4j"]