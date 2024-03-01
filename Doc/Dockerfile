# Use a base image with Java installed (e.g., OpenJDK 11)
FROM openjdk:17

# Set environment variables for Maven version and installation path
ENV MAVEN_VERSION 3.9.6
ENV MAVEN_HOME /usr/lib/mvn
ENV PATH $MAVEN_HOME/bin:$PATH

# Install Maven
RUN mkdir -p $MAVEN_HOME \
  && curl -fsSL http://archive.apache.org/dist/maven/maven-3/$MAVEN_VERSION/binaries/apache-maven-$MAVEN_VERSION-bin.tar.gz \
  | tar -xzC $MAVEN_HOME --strip-components=1

# Verify installation
RUN mvn -version

# Your application's Dockerfile commands follow...
