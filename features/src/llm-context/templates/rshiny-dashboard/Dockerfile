FROM rocker/shiny:4.3.2@sha256:882ffd767bc97fa310da50137f7539f548978a354b5e9d1e87b0f6741b81a44b

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
