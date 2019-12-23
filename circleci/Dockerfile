FROM mossuru777/vsenv:circleci-latest
MAINTAINER Mossuru777 "mossuru777@gmail.com"

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

# Define mountable directories
VOLUME ["/var/www/html"]

# Define default command
CMD ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]

# Expose port
EXPOSE 80
