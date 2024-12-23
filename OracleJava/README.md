# Oracle Java in Containers

This repository contains sample container configurations to facilitate installation and environment setup for DevOps users. This project provides container images based on Oracle Linux for JDK versions 23, 21, 17, 11 and 8 as well as Server JRE 8.

Oracle Java Server JRE provides the features from Oracle Java JDK commonly required for server-side applications (i.e. Running a Java EE application server). For more information about Server JRE, visit the [Understanding the Server JRE blog entry](https://blogs.oracle.com/java-platform-group/understanding-the-server-jre) from the Java Product Management team.

## Building the Oracle Java base image

For JDK 23 and 21 the required JDK binaries will be downloaded from [Oracle](https://www.oracle.com/javadownload) as part of the build using curl.

For JDK 17, JDK 11, and JDK 8 you must first download the linux x64 or linux aarch64 compressed archive (tar.gz), for Server JRE 8 you must download the linux x64 compressed archive, from [https://oracle.com/javadownload](https://www.oracle.com/javadownload) and place it in the same directory as the corresponding Dockerfile.

e.g. for JDK 17 download jdk-17[X]_linux-x64_bin.tar.gz into OracleJava/17, for Server JRE 8 download server-jre-8uXXX-linux-x64.tar.gz into OracleJava/8/serverjre

To build the container image run `docker build`. Tag it with the correct version number.

e.g. For JDK 23 run

```bash
cd ../OracleJava/23
docker build --tag oracle/jdk:23 .
```

for Server JRE 8 run

```bash
cd ../OracleJava/8/serverjre
docker build --tag oracle/serverjre:8 .
```

The right command with the correct tag is already scripted in `build.sh` so you can alternatively run:

```bash
bash build.sh
```

### Parent image OS version

The Oracle Java image for JDK 23 uses `oraclelinux:9` as the parent image.

The Oracle Java image for JDK  21 and 17 use `oraclelinux:8` as the parent image.

JDK 21 allows for optionally building on `oraclelinux:9` by using `Dockerfile.9` rather than `Dockerfile`.

The Oracle Java image for JDK 11, JDK 8, and Server JRE 8 use `oraclelinux:7-slim` as the parent image.

JDK 11, JDK 8, and Server JRE 8 allow for optionally building on `oraclelinux:8` by using `Dockerfile.8` rather than `Dockerfile`.

e.g. to build JDK 11 with Oracle Linux 8 rather than the default Oracle Linux 7 run

```bash
cd ../OracleJava/11
docker build --file Dockerfile.8 --tag oracle/jdk:11-oraclelinux8 .
```

On JDK 11, JDK 8, and Server JRE 8 `build.sh` can be used to build on Oracle Linux 8, by passing `8`.
e.g.

```bash
cd ../OracleJava/11
bash build.sh 8
```

The script `build.sh` will tag the images it creates with the JDK version, and with the operating system and OS version e.g., '17-ol8'.

## Licenses

JDK 23 and 21 are downloaded, as part of the build process, from the [Oracle Website](https://www.oracle.com/javadownload) under the [Oracle No-Fee Terms and Conditions (NFTC)](https://java.com/freeuselicense).

For building JDK 17, JDK 11, JDK 8, and Server JRE 8 you must first download the corresponding Java Runtime from the [Oracle Website](https://www.oracle.com/javadownload) and accept the license indicated on that page.

All scripts and files hosted in this project and GitHub [`docker/OracleJava`](./) repository, required to build the container images are, unless otherwise noted, released under the [UPL 1.0](https://oss.oracle.com/licenses/upl/) license.

## Customer Support

Oracle offers support for JDK 23, JDK 21, JDK 17, JDK 11, and JDK 8 (JDK and Server JRE) when running on certified operating systems in a container. For additional details on the JDK Certified System Configurations, please refer to the [Oracle Java SE Certified System Configuration Pages](https://www.oracle.com/technetwork/java/javaseproducts/documentation/index.html#sysconfig).
