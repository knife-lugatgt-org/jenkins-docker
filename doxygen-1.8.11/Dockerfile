FROM debian:stable
ARG JENKINSPW=jenkins

RUN apt-get update && \
	DEBIAN_FRONTEND=noninteractive apt-get install -y \
		git \
		graphviz \
		openjdk-7-jre-headless \
		openssh-server && \
	apt-get clean && \
	rm -rf /var/lib/apt/lists/*

ADD doxygen-1.8.11.linux.bin.tar.gz /opt
RUN ln -s /opt/doxygen-1.8.11/bin/doxygen /usr/local/bin/doxygen

# Jenkins user.
RUN useradd -m jenkins && \
	echo "jenkins:$JENKINSPW" | chpasswd

# SSH server.
RUN mkdir -p /var/run/sshd && \
	sed -i 's|session    required     pam_loginuid.so|session    optional     pam_loginuid.so|g' /etc/pam.d/sshd
EXPOSE 22
CMD ["/usr/sbin/sshd", "-D"]
