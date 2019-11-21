FROM python:3.7

ARG VERSION="3.13.1"
ARG SPADESPATH="SPAdes-${VERSION}-Linux"

# Metadata
LABEL container.base.image="python:3.7"
LABEL software.name="SPAdes"
LABEL software.version=${VERSION}
LABEL software.description="Genome Assembler"
LABEL software.website="http://cab.spbu.ru/software/spades/"
LABEL software.documentation="https://github.com/ablab/spades/blob/spades_3.13.1/README.md"
LABEL software.license="NA"
LABEL tags="Genomics"

# RUN apt-get -y update && \
#    apt-get -y install zlib1g-dev gnuplot && \
#    apt-get clean

RUN pip3 install boto3 awscli


# This will install Spades in dir: /SPAdes-${VERSION}-Linux/bin
RUN wget http://cab.spbu.ru/files/release3.13.1/SPAdes-3.13.1-Linux.tar.gz && \
    tar -xzf SPAdes-${VERSION}-Linux.tar.gz

ENV PATH="${SPADESPATH}/bin:$PATH"
ENV LD_LIBRARY_PATH="/usr/local/lib:/usr/lib:/isaac/libexec:${LD_LIBRARY_PATH}"

COPY spades/src/run_spades.py /
COPY common_utils /common_utils

ENTRYPOINT ["python3", "/run_spades.py"]
