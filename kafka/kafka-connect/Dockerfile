FROM quay.io/strimzi/kafka:latest-kafka-3.9.0

USER root

# Debug: Check what we're copying
RUN echo "=== Current directory before copy ===" && pwd && ls -la

# Create plugin directories
RUN mkdir -p /opt/kafka/plugins/kafka-connect-jdbc \
    && mkdir -p /opt/kafka/plugins/kafka-connect-s3

# Debug: Verify directories were created
RUN echo "=== Directories created ===" && find /opt/kafka/plugins -type d

# Copy lib directory
COPY lib/ /opt/kafka/plugins/kafka-connect-jdbc/

# Debug: Check what was copied
RUN echo "=== After copying lib/ ===" && ls -la /opt/kafka/plugins/kafka-connect-jdbc/

# Copy S3 JAR to its directory
RUN find /opt/kafka/plugins/kafka-connect-jdbc/ -name "*s3*" -exec cp {} /opt/kafka/plugins/kafka-connect-s3/ \; || echo "No S3 files found"

# Final verification
RUN echo "=== Final structure ===" \
    && find /opt/kafka/plugins -name "*.jar" | head -10 \
    && echo "=== Oracle driver ===" \
    && find /opt/kafka/plugins -name "*ojdbc*"

# Set environment and permissions
ENV CONNECT_PLUGIN_PATH=/opt/kafka/plugins
RUN chown -R 1001:1001 /opt/kafka/plugins

USER 1001