# docker-openjdk
Repository contains docker builds for OpenJDK   

## Versions
### JDK 11 (Alpine)

According to https://jdk.java.net/11/
> > The Alpine Linux build previously available on this page was removed as of JDK 11 GA. 
It’s not production-ready because it hasn’t been tested thoroughly enough to be considered a GA build

Image with the full JDK is ~300MB. This build uses jlink to create custom JRE with modules required to run microservices based on Spring Boot 2.

Size ~ 60MB 