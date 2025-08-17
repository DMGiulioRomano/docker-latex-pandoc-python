FROM debian:12.11-slim@sha256:2424c1850714a4d94666ec928e24d86de958646737b1d113f5b2207be44d37d8

RUN apt-get update && apt-get install -y --no-install-recommends \
    ca-certificates \
    perl \
    wget \
    fontconfig \
    make \
    gcc \
    g++ \
    git \
    openssh-client \
    rsync \
    curl \
    && rm -rf /var/lib/apt/lists/*

RUN echo "selected_scheme scheme-basic" > /tmp/texlive.profile && \
    TEXLIVE_MIRROR=http://mirror.ctan.org/systems/texlive/tlnet && \
    TEXLIVE_INSTALLER=install-tl-unx.tar.gz && \
    wget -O /tmp/$TEXLIVE_INSTALLER $TEXLIVE_MIRROR/$TEXLIVE_INSTALLER && \
    mkdir /tmp/texlive && \
    tar -xzf /tmp/$TEXLIVE_INSTALLER -C /tmp/texlive --strip-components=1 && \
    /tmp/texlive/install-tl -profile /tmp/texlive.profile && \
    rm -rf /tmp/texlive /tmp/$TEXLIVE_INSTALLER

ENV PATH="/usr/local/texlive/2025/bin/x86_64-linux:${PATH}"
RUN tlmgr update --self && \
    tlmgr install \
        collection-basic \
        collection-latex \
        collection-latexrecommended \
        collection-latexextra \
        collection-luatex \
        collection-mathscience \
        collection-pictures \
        collection-bibtexextra \
        collection-publishers \
        collection-fontsextra \
        collection-fontsrecommended \
        collection-langenglish \
        collection-langeuropean \
        collection-langitalian \
        collection-langgerman \
        collection-langfrench \
        collection-langspanish \
        collection-langpolish \
        collection-langportuguese \
        hyphen-english \
        hyphen-french \
        hyphen-german \
        hyphen-italian \
        hyphen-spanish \
        hyphen-polish \
        hyphen-portuguese \
        latexmk \
        biber

RUN apt-get update && apt-get install -y --no-install-recommends \
    pandoc \
    python3 \
    python3-pip \
    && rm -rf /var/lib/apt/lists/*

RUN pip3 install --no-cache-dir --upgrade pip && \
    pip3 install --no-cache-dir PyYAML liquidpy

ENV PATH $PATH:/usr/local/texlive/2025/bin/x86_64-linux
WORKDIR /data
VOLUME ["/data"]
