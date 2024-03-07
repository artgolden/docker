FROM rocker/tidyverse
  
RUN mkdir /home/analysis

RUN apt-get update && apt-get install -y  --no-install-recommends \
    libbz2-dev liblzma-dev libcurl4 libglpk-dev \
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
    libgsl-dev libxt-dev libcairo2-dev \
    && rm -rf /var/lib/apt/lists/*
RUN R -e "install.packages('BiocManager')"
RUN R -e "install.packages('devtools')"
RUN R -e "install.packages(c('markdown', 'rmdformats'))"
RUN R -e "install.packages(c('ggpubr', 'patchwork'))"
RUN R -e "install.packages(c('scuttle', 'pheatmap', 'future'))"
RUN R -e "install.packages('hexbin')"
RUN R -e "devtools::install_github('GreenleafLab/chromVARmotifs')"
RUN R -e "BiocManager::install(c('EnsDb.Mmusculus.v79'))"
RUN R -e "BiocManager::install(c('clusterProfiler', 'biomaRt'))"
RUN R -e "BiocManager::install('BSgenome.Mmusculus.UCSC.mm10')"


ARG GITHUB_TOKEN
RUN R -e "Sys.setenv(GITHUB_PAT='$GITHUB_TOKEN')"
RUN R -e "devtools::install_github('GreenleafLab/ArchR', ref='release_1.0.2', repos = BiocManager::repositories())"
RUN R -e "ArchR::installExtraPackages()"


RUN apt-get update && apt-get install --no-install-recommends -y python3 python3-dev python3-pip python3-wheel build-essential && \
   apt-get clean && rm -rf /var/lib/apt/lists/*
RUN pip3 install --no-cache-dir MACS2
EXPOSE 8787 8788

ENV USER rstudio
