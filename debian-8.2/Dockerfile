FROM debian:8.2
ARG JENKINSPW=jenkins

RUN apt-get update && \
	DEBIAN_FRONTEND=noninteractive apt-get install -y \
		build-essential \
		clang \
		cmake \
		gettext \
		git \
		openjdk-7-jre-headless \
		openssh-server \
		pkg-config && \
	DEBIAN_FRONTEND=noninteractive apt-get install -y \
		libalut-dev \
		libcurl4-gnutls-dev \
		libboost-filesystem-dev \
		libboost-locale-dev \
		libboost-log-dev \
		libboost-thread-dev \
		libopenal-dev \
		libsdl2-dev \
		libsdl2-image-dev \
		libsdl2-ttf-dev \
		libyaml-dev \
		libxdg-basedir-dev && \
	apt-get clean && \
	rm -rf /var/lib/apt/lists/*

# Config files for build.
RUN mkdir /build
COPY compiler-gcc.properties /build
COPY compiler-clang.properties /build

# Jenkins user.
RUN useradd -m jenkins && \
	echo "jenkins:$JENKINSPW" | chpasswd

# SSH server.
RUN mkdir -p /var/run/sshd && \
	sed -i 's|session    required     pam_loginuid.so|session    optional     pam_loginuid.so|g' /etc/pam.d/sshd
EXPOSE 22
CMD ["/usr/sbin/sshd", "-D"]
