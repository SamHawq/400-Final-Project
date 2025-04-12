# Start with Jenkins base image (Alpine)
FROM jenkins/jenkins:alpine

USER root

# Install dependencies
RUN apk add --no-cache docker openrc curl tar unzip

# ----------------------------
# Install JDK 11 (Temurin)
# ----------------------------
ENV JDK_VERSION=11.0.22_7
ENV JDK_BUILD=jdk-11.0.22+7
ENV JDK_DIR=/opt/jdk
ENV JAVA_HOME=${JDK_DIR}
ENV PATH="${JAVA_HOME}/bin:${PATH}"
ENV JDK_URL=https://github.com/adoptium/temurin11-binaries/releases/download/${JDK_BUILD}/OpenJDK11U-jdk_x64_linux_hotspot_${JDK_VERSION}.tar.gz

RUN mkdir -p ${JDK_DIR} && \
    curl -L ${JDK_URL} -o /tmp/openjdk.tar.gz && \
    tar -xzf /tmp/openjdk.tar.gz -C /tmp && \
    mv /tmp/jdk-*/* ${JDK_DIR} && \
    rm -rf /tmp/openjdk.tar.gz /tmp/jdk-*

# ----------------------------
# Install Gradle 7.6.1
# ----------------------------
ENV GRADLE_VERSION=7.6.1
ENV GRADLE_HOME=/opt/gradle
ENV PATH="${GRADLE_HOME}/bin:${PATH}"
ENV GRADLE_DIST=https://services.gradle.org/distributions/gradle-${GRADLE_VERSION}-bin.zip

RUN mkdir -p ${GRADLE_HOME} && \
    curl -L ${GRADLE_DIST} -o /tmp/gradle.zip && \
    unzip -d /opt /tmp/gradle.zip && \
    mv /opt/gradle-${GRADLE_VERSION}/* ${GRADLE_HOME} && \
    rm -rf /tmp/gradle.zip /opt/gradle-${GRADLE_VERSION}

# Verify installations
RUN java -version && gradle --version