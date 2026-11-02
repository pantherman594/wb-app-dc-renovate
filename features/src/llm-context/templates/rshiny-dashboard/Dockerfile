FROM rocker/shiny:4.6.2@sha256:ff9c0fd8bbb20c40556cd97875d3e34567a90d4cfe00f15aad5cf32dde9403bd

# Install system dependencies
RUN apt-get update && apt-get install -y --no-install-recommends \
    libcurl4-openssl-dev \
    libssl-dev \
    libxml2-dev \
    fuse \
    && rm -rf /var/lib/apt/lists/*

# Install R packages
RUN R -e "install.packages(c( \
    'shiny', \
    'shinydashboard', \
    'DT', \
    'plotly', \
    'ggplot2', \
    'dplyr', \
    'tidyr', \
    'bigrquery', \
    'googleCloudStorageR' \
), repos='https://cran.rstudio.com/')"

# Create app directory
RUN mkdir -p /srv/shiny-server/app

# Copy application
COPY app/ /srv/shiny-server/

# Copy Shiny server config
COPY shiny-server.conf /etc/shiny-server/shiny-server.conf

# Set permissions
RUN chown -R shiny:shiny /srv/shiny-server

EXPOSE 3838

USER shiny

CMD ["/usr/bin/shiny-server"]
