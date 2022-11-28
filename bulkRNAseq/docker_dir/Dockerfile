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
    libgsl-dev libxt-dev libcairo2-dev
RUN R -e "install.packages('BiocManager')"
RUN R -e "BiocManager::install(c('EnhancedVolcano'))"
RUN R -e "BiocManager::install(c('RColorBrewer', 'ComplexHeatmap', 'circlize', 'digest', 'cluster'))"
RUN R -e "install.packages(c('markdown', 'rmdformats'))"
RUN R -e "install.packages(c('ggpubr', 'patchwork'))"
RUN R -e "install.packages(c('pheatmap', 'future'))"
RUN R -e "BiocManager::install(c('DESeq2'))"

EXPOSE 8787 8788

ENV USER rstudio
