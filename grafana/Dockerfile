# grafana/Dockerfile

# Use Debian Bullseye as the base image
FROM debian:bullseye

# Install necessary packages including gnupg for adding repositories
RUN apt-get update && apt-get install -y \
    wget \
    ca-certificates \
    gnupg \
    openssl \
    apt-transport-https \
    software-properties-common \
    && rm -rf /var/lib/apt/lists/*

# Add Grafana's APT key and repository
RUN wget -q -O - https://packages.grafana.com/gpg.key | apt-key add - \
    && add-apt-repository "deb https://packages.grafana.com/oss/deb stable main"

# Install Grafana
RUN apt-get update && apt-get install -y grafana \
    && rm -rf /var/lib/apt/lists/*

# Generate a self-signed SSL certificate
RUN mkdir -p /etc/grafana/ssl && \
    openssl req -x509 -nodes -days 365 -newkey rsa:2048 \
    -keyout /etc/grafana/ssl/grafana.key \
    -out /etc/grafana/ssl/grafana.crt \
    -subj "/C=MO/ST=KH/L=KH/O=1337/OU=1337/CN=localhost/UID=user"

# Copy custom configuration file
COPY ./config/grafana.ini /etc/grafana/grafana.ini
# COPY ./config/provisioning/datasources/datasources.yml /etc/grafana/provisioning/datasources/datasources.yml
# COPY ./config/provisioning/dashboards/dashboards.yml /etc/grafana/provisioning/dashboards/dashboards.yml
# COPY ./dashboards/ /etc/grafana/provisioning/dashboards/

# Start Grafana
CMD ["/usr/sbin/grafana-server", "--config=/etc/grafana/grafana.ini", "--homepath=/usr/share/grafana"]
