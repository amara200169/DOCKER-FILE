# Use the official Jenkins LTS image from Docker Hub
FROM jenkins/jenkins:lts
# Set environment variables for Jenkins
ENV JAVA_OPTS="-Djenkins.install.runSetupWizard=false"
# Switch to the root user to install additional packages
USER root
# Update the package list and install any necessary packages
RUN apt-get update -y
    
# Create a directory for Jenkins data (optional, for persistent storage)
RUN mkdir -p /var/jenkins_home
# Set the correct permissions for the Jenkins user
RUN chown -R jenkins:jenkins /var/jenkins_home
# Start Jenkins by default when the container runs
ENTRYPOINT ["/usr/bin/tini", "--", "/usr/local/bin/jenkins.sh"]
    
# Allow Jenkins user to use sudo without a password
RUN echo "jenkins ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers
# Switch back to the Jenkins user
USER jenkins
# Expose port 8080 for the Jenkins web interface
EXPOSE 8080
# Expose port 60000 for Jenkins agent connections
EXPOSE 70000
# Start Jenkins
CMD ["jenkins"]
