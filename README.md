# busybox-glibc-rpi
Busybox container with glibc for raspeberry pi board (all in just 4,5MB).

>Note that this image is not for production and should be used only develop and test purposes.

This image has been created using [Buildroot](https://buildroot.org/) tool. You can find the buildroot config file in the buildroot folder together with the configuration used for busybox.

This source repo is linked to automated build feature actived in Docker Hub so refer to [antvale/busybox-glibc-rpi] (https://hub.docker.com/r/antvale/busybox-glibc-rpi/) image name if you want to pull the latest tag from Docker Hub public reposiroty.
 
To test the image you can run this simple docker command line from raspberry board 
`docker run antvale/busybox-glibc-rpi ls -l /lib/`
that will automatically pull the latest image from official Docker Hub and list the content of lib folder, that's, the glibc libraries. 

####What do you do with this image?
You can use it as tiny basis to build other images that require glibc to run (as java virtual machine,...). 
This image with its only 4,5MB is able to run the latest version of Oracle JRE. As results, you can build armhf 32-bit JVM docker images saving a lot of space compared to other images based on jessie or wheezy.
 
####How can you build a JRE docker image?
There are several ways to build a jvm image starting FROM [antvale/busybox-glibc-rpi] (https://hub.docker.com/r/antvale/busybox-glibc-rpi/) as creating a new Dockerfile able to download autonatically a given JRE or JDK version from official Oracle site and unarchiving it in your hand made images or downloading manually the desired JRE version and then ADD or COPY it in the the docker image.  
In the first event you should install curl and tar utils and following the steps described for example here https://developer.atlassian.com/blog/2015/08/minimal-java-docker-containers/. The below section "How to build a JRE docker image" instead describes how to create this image using the second approach. 

####How to build a Oracle JRE docker image.
1. Go to [Oracle OTN](http://www.oracle.com/technetwork/java/embedded/embedded-se/downloads/javase-embedded-downloads-2209751.html) site to download the latest embedded ARMv7 jre: ejdk-8u101-linux-arm-sflt.tar.gz
2. Accept the Oracle license and download the tarball in your local folder.
3. Unpack the file through `tar xfv ejdk-8u101-linux-arm-sflt.tar.gz` command. 
4. Create a Dockerfile in the local folder like that shown below to copy in the image the full embedded jre
5. Build the image using `docker build -t <image-id:tag> .` (please, replace the `<image:tag>` with your identifier).

Dockerfile 
~~~docker
FROM antvale/busybox-glibc-rpi 
ADD ejdk1.8.0_101/linux_arm_sflt/jre /opt/jre 
ENV JAVA_HOME /opt/jre 
ENV PATH ${PATH}:${JAVA_HOME}/bin 

To test the new image you can run the docker command `docker run <image-id:tag> java -version` that, if everything is ok, shows the following output:
*java version "1.8.0_101" 
Java(TM) SE Embedded Runtime Environment (build 1.8.0_101-b13, headless) 
Java HotSpot(TM) Embedded Client VM (build 25.101-b13, mixed mode)* 

The final image will be only 66.01MB of size including everything is required to run a java application.

####Requirements
This images has been tested on RPI version 3 board with 32bit armv7 arch, Little Endian order, Raspbian GNU/Linux 8 (jessie)/4.4.11-v7+ kernel

####Versions of tools and libreries used to build the image:
* Ubuntu 16.04.1 LTS (Xenial Xerus)
* Buildroot (default cross-compiler, kerner headers 4.4.x):  buildroot-2016.05 
* Busybox 1.24.2 32bit
* Glibc 2.22 32bit
