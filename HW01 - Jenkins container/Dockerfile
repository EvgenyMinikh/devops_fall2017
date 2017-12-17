# Use openjdk image as a source
FROM openjdk:latest

#================================
#===== List of arguments ========

# Directory with lenkins.war file
ARG start_folder=/usr/bin/jenkins

# Directory with Jenkins logs
ARG log_folder=/var/log/jenkins

# Folder with Jenkins data in user home folder
ARG home_folder=/home/jenkins/.jenkins

# Latest jenkins.war file
ARG war_url=http://mirrors.jenkins.io/war-stable/latest/jenkins.war
#================================

# Add additional info to the image
LABEL maintainer="Evgeny Minikh <evgeny.minih@gmail.com>"
LABEL description="My first container with Jenkins"

# Create necessary folders and add access rights for them
RUN useradd -m jenkins && \
	mkdir -p ${start_folder} && \
	mkdir -p ${log_folder} && \
	mkdir -p ${home_folder} && \
	chown -R jenkins:jenkins ${home_folder} && \
	chown -R jenkins:jenkins ${log_folder}

# Copy build of Jenkins into the container
ADD ${war_url} ${start_folder}/

RUN chown -R jenkins:jenkins ${start_folder}

# Open port 8080
EXPOSE 8080

# Change user to execute next commands
USER jenkins
WORKDIR ${start_folder}

VOLUME ${home_folder} ${log_folder}

# When container runs, execute command "java -jar jenkins.war" to start Jenkins
ENTRYPOINT ["java"]
CMD ["-jar", "jenkins.war"]
