FROM quay.io/strimzi/kafka:latest-kafka-3.9.0

USER root

# Create plugin directories
RUN mkdir -p /opt/kafka/plugins/kafka-connect-jdbc \
    && mkdir -p /opt/kafka/plugins/kafka-connect-s3

# Copy all JDBC files first
COPY lib/jdbc/* /opt/kafka/plugins/kafka-connect-jdbc/

# Also copy S3 files to S3 directory
COPY lib/s3/* /opt/kafka/plugins/kafka-connect-s3/

# Set permissions
RUN chown -R 1001:1001 /opt/kafka/plugins

USER 1001