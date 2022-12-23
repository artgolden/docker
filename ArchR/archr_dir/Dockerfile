FROM rocker/tidyverse
  
RUN mkdir /home/analysis

RUN apt-get update && apt-get install -y libbz2-dev liblzma-dev libcurl4 libglpk-dev \
    openssl libssl-dev \
    libssl-dev \
    libjq-dev \
    libprotobuf-dev \
    protobuf-compiler \
    make \
    libgeos-dev \
    libudunits2-dev \
    libgdal-dev \
    gdal-bin \
    libproj-dev \
    libv8-dev \
    libgsl-dev libxt-dev libcairo2-dev python3 python3-pip
RUN pip3 install --upgrade pip
RUN pip3 install --trusted-host pypi.python.org numpy==1.22.1 \
    && pip3 install --trusted-host pypi.python.org MACS2==2.2.7.1
RUN R -e "install.packages('BiocManager')"
RUN R -e "install.packages('devtools')"
RUN R -e "install.packages(c('markdown', 'rmdformats'))"
RUN R -e "install.packages(c('ggpubr', 'patchwork'))"
RUN R -e "install.packages(c('scuttle', 'pheatmap', 'future'))"
RUN R -e "BiocManager::install(c('EnsDb.Mmusculus.v79'))"
RUN R -e "BiocManager::install(c('clusterProfiler', 'biomaRt'))"
RUN R -e "BiocManager::install('BSgenome.Mmusculus.UCSC.mm10')"

ARG GITHUB_TOKEN
RUN R -e "Sys.setenv(GITHUB_PAT='$GITHUB_TOKEN')"
RUN R -e "devtools::install_github('GreenleafLab/ArchR', ref='release_1.0.2', repos = BiocManager::repositories())"
RUN R -e "ArchR::installExtraPackages()"
RUN R -e "devtools::install_github('GreenleafLab/chromVARmotifs')"
RUN R -e "install.packages('hexbin')"
EXPOSE 8787 8788

ENV USER rstudio
