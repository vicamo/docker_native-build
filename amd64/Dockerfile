# DO NOT EDIT!!! GENERATED FROM Dockerfile.template.
FROM vicamo/debian:testing-amd64

ENV LAARID_USER=laarid
ENV LAARID_HOME=/home/${LAARID_USER}

RUN apt-get update -qq \
	&& apt-get upgrade -y \
	&& apt-get install --no-install-recommends -y \
		apt-transport-https \
		build-essential \
		ca-certificates \
		ccache \
		debhelper \
		devscripts \
		equivs \
		git \
		libc6-dev \
		libfile-fcntllock-perl \
		lintian \
		sudo

RUN echo "deb [allow-insecure=yes] http://dl.bintray.com/laarid/main testing main" | \
		tee /etc/apt/sources.list.d/bintray.list; \
	(echo "Package: *"; echo "Pin: origin \"dl.bintray.com\""; echo "Pin-Priority: 1000") | \
		tee /etc/apt/preferences.d/bintray.pref; \
	apt-get update -qq

# Cannot fetch key on mips/mipsel.
# See https://github.com/laarid/docker/issues/11
#
# 	&& apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 379CE192D401AB61

RUN useradd --comment 'LAARiD Development Account' \
		--home ${LAARID_HOME} --create-home \
		--shell /bin/bash \
		${LAARID_USER} \
	&& (echo "${LAARID_USER}:laarid" | chpasswd) \
	&& adduser ${LAARID_USER} sudo \
	&& (echo "${LAARID_USER} ALL=NOPASSWD: ALL" > /etc/sudoers.d/laarid) \
	&& chmod 0440 /etc/sudoers.d/laarid

VOLUME ["${LAARID_HOME}"]
WORKDIR ${LAARID_HOME}
USER ${LAARID_USER}
