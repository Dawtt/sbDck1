

### Notes from https://spring.io/guides/gs/spring-boot-docker/#initial ###
This Dockerfile is very simple, but that’s all you need to run a Spring Boot app with no frills: just Java and a JAR file. The project JAR file is ADDed to the container as "app.jar" and then executed in the ENTRYPOINT

We added a VOLUME pointing to "/tmp" because that is where a Spring Boot application creates working directories for Tomcat by default. The effect is to create a temporary file on your host under "/var/lib/docker" and link it to the container under "/tmp". This step is optional for the simple app that we wrote here, but can be necessary for other Spring Boot applications if they need to actually write in the filesystem.


To reduce Tomcat startup time we added a system property pointing to "/dev/urandom" as a source of entropy.

if you are using boot2docker you need to run it first before you do anything with the Docker command line or with the build tools (it runs a daemon process that handles the work for you in a virtual machine).


pom.xml docker entry; The configuration specifies 3 things:

The repository with the image name, which will end up here as  springio/gs-spring-boot-docker

The name of the jar file, exposing the Maven configuration as a build argument for docker.

Optionally, the image tag, which ends up as latest if not specified. It can be set to the artifact id if desired.



Add dockerFile push to pom.xml:
<executions>
	<execution>
		<id>default</id>
		<phase>install</phase>
		<goals>
			<goal>build</goal>
			<goal>push</goal>
		</goals>
	</execution>
</executions>

