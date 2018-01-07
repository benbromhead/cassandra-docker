FROM debian:jessie

COPY dagi /usr/local/bin/

RUN echo "deb http://http.debian.net/debian jessie-backports main" > /etc/apt/sources.list.d/jessie-backports.list

# common set of packages shared by all
RUN dagi	krb5-locales \
    		libexpat1 \
    		libffi6 \
    		libgmp10 \
    		libgnutls-deb0-28 \
    		libgssapi-krb5-2 \
    		libhogweed2 \
    		libk5crypto3 \
    		libkeyutils1 \
    		libkrb5-3 \
    		libkrb5support0 \
    		libnettle4 \
    		libp11-kit0 \
    		libsqlite3-0 \
    		libssl1.0.0 \
    		libtasn1-6 \
    		libxml2 \
    		openssl \
    		sgml-base \
    		ucf \
    		xml-core \
    		locales \
    		curl \
			python libpython-stdlib  python-minimal python-support python-pip \
			mime-support \
			ntp \
			ca-certificates \
			bzip2 \
			netcat \
			wget \
			libjemalloc1 \
			daemontools

RUN CASS_DRIVER_NO_CYTHON=1 pip install --install-option="--no-extensions" cassandra-driver

ENV PATH /opt/bin:$PATH

# make the "en_US.UTF-8" locale
RUN localedef -i en_US -c -f UTF-8 -A /usr/share/locale/locale.alias en_US.UTF-8
ENV LANG en_US.utf8

RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys EEA14886 \
    && echo "deb http://ppa.launchpad.net/webupd8team/java/ubuntu trusty main" >> /etc/apt/sources.list.d/webupd8team-java.list \
    && echo "deb-src http://ppa.launchpad.net/webupd8team/java/ubuntu trusty main" >> /etc/apt/sources.list.d/webupd8team-java.list \
    && echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | /usr/bin/debconf-set-selections

RUN dagi oracle-java8-installer \
    && rm -r /var/cache/oracle-jdk8-installer

COPY local_policy.jar US_export_policy.jar /usr/lib/jvm/java-8-oracle/jre/lib/security/

COPY install-cassandra /tmp/install-cassandra

#RUN /tmp/install-cassandra @@APACHE_CASSANDRA_VERSION@@ @@CUSTOM_BUILD@@
