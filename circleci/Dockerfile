FROM mossuru777/vsenv:circleci-latest
MAINTAINER Mossuru777 "mossuru777@gmail.com"

# Switch User to root
USER root

# Setup
ENV DEBIAN_FRONTEND noninteractive
RUN apt-get -y update \
    && apt-get -y upgrade \
    && apt-get -y install --no-install-recommends \
        apache2

# Enable site configuration
COPY localhost.conf /etc/apache2/sites-available/localhost.conf
RUN a2enmod cgi \
    && a2dissite 000-default \
    && a2ensite localhost \
    && service apache2 stop

# Switch perl
RUN mv /usr/bin/perl /usr/bin/perl.orig \
    && ln -s /usr/local/bin/perl /usr/bin/perl

# Switch User to circleci
WORKDIR /home/circleci
USER circleci

# Define default command
CMD ["sudo", "-u", "root", "/usr/sbin/apache2ctl", "-D", "FOREGROUND"]

# Expose port
EXPOSE 80
