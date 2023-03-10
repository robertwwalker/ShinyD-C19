# get shiny server plus tidyverse packages image
FROM rocker/geospatial:latest
# system libraries of general use
# FROM openanalytics/r-shiny
RUN apt-get update && apt-get install -y \
    sudo \
    pandoc \
    pandoc-citeproc \
    libcurl4-gnutls-dev \
    libcairo2-dev \
    libxt-dev \
    libssl-dev \
    libssh2-1-dev \
    libxml2-dev \
    libudunits2-dev \
    libsasl2-dev \
    libv8-dev
 
# install R packages required 
# (change it depending on the packages you need)
RUN R -e "install.packages(c('rmarkdown','shiny','sp','patchwork','tidyverse','knitr','plotly','flexdashboard','ggrepel','hrbrthemes','ggthemes','lubridate','magrittr','patchwork','leaflet','tigris','tidycensus'), repos='http://cran.rstudio.com/')"
# Copy configuration files into the Docker image
# COPY shiny-server.conf  /etc/shiny-server/shiny-server.conf
# COPY /app/index.Rmd /srv/shiny-server/
# RUN rm /srv/shiny-server/index.html
# make directory and copy Rmarkdown flexdashboard file in it
# RUN mkdir -p /bin
# COPY /app/index.Rmd    /bin/index.Rmd
# COPY shiny-server.conf  /etc/shiny-server/shiny-server.conf
# COPY /app /srv/shiny-server/
# RUN rm /srv/shiny-server/index.html
# Make the ShinyApp available at port 3838
EXPOSE 3838
# Copy further configuration files into the Docker image
# COPY shiny-server.sh /usr/bin/shiny-server.sh
# RUN ["chmod", "+x", "/usr/bin/shiny-server.sh"]
# CMD ["/usr/bin/shiny-server.sh"]
# RUN mkdir -p /bin
COPY /app/index.Rmd    /srv/shiny-server/index.Rmd


# make all app files readable (solves issue when dev in Windows, but building in Ubuntu)
# RUN chmod -R 755 /bin

# expose port on Docker container
# EXPOSE 3838

# run flexdashboard as localhost and on exposed port in Docker container
CMD ["R", "-e", "rmarkdown::run('/srv/shiny-server/index.Rmd', shiny_args = list(port = 3838, host = '0.0.0.0'))"]
