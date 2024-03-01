# First stage: Install Docker CLI
FROM ubuntu:latest AS docker_installation

# Install Docker CLI
RUN apt-get update && apt-get install -y \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg \
    lsb-release \
    software-properties-common

RUN curl -fsSL https://download.docker.com/linux/ubuntu/gpg | apt-key add -
RUN add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
RUN apt-get update && apt-get install -y docker-ce-cli

# Verify Docker CLI installation
RUN docker --version

# Second stage: Install Maven
FROM openjdk:17 AS maven_installation

# Set the Maven version
ENV MAVEN_VERSION 3.8.4
ENV MAVEN_HOME /usr/share/maven

# Install Maven
RUN mkdir -p $MAVEN_HOME \
  && curl -fsSL https://archive.apache.org/dist/maven/maven-3/${MAVEN_VERSION}/binaries/apache-maven-${MAVEN_VERSION}-bin.tar.gz \
  | tar -xzC $MAVEN_HOME --strip-components=1 \
  && ln -s $MAVEN_HOME/bin/mvn /usr/bin/mvn

# Verify Maven installation
# Final stage: Build your application
FROM openjdk:17

# Copy Maven from the Maven installation stage
COPY --from=maven_installation /usr/share/maven /usr/share/maven

# Copy Docker CLI from the Docker installation stage
COPY --from=docker_installation /usr/bin/docker /usr/bin/docker

# Add Maven to the PATH
ENV PATH="/usr/share/maven/bin:${PATH}"

# Verify Maven installation
RUN mvn --version

# Continue with your application build process