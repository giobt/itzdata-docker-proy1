#
# MySQL Dockerfile
#
# https://github.com/dockerfile/mysql
#

# Pull base image.
FROM ubuntu

# Install.
RUN mkdir -p /var/run/mysqld
	
# Install MySQL.
RUN apt-get update && \
  DEBIAN_FRONTEND=noninteractive apt-get install -y mysql-server
RUN rm -rf /var/lib/apt/lists/*
RUN sed -i 's/^\(bind-address\s.*\)/# \1/' /etc/mysql/my.cnf
RUN sed -i 's/^\(log_error\s.*\)/# \1/' /etc/mysql/my.cnf
RUN echo "mysqld_safe &" > /tmp/config
RUN echo "mysqladmin --silent --wait=30 ping || exit 1" >> /tmp/config
RUN echo "mysql -e 'GRANT ALL PRIVILEGES ON *.* TO \"root\"@\"%\" WITH GRANT OPTION;'" >> /tmp/config
RUN bash /tmp/config
RUN rm -f /tmp/config
  
# Define mountable directories.
VOLUME ["/etc/mysql", "/var/lib/mysql"]

# Define working directory.
WORKDIR /data

# Define default command.
CMD ["mysqld_safe"]

# Expose ports.
EXPOSE 3306