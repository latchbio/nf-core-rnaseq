# DO NOT CHANGE
from 812206152185.dkr.ecr.us-west-2.amazonaws.com/latch-base:fe0b-main

workdir /tmp/docker-build/work/

shell [ \
    "/usr/bin/env", "bash", \
    "-o", "errexit", \
    "-o", "pipefail", \
    "-o", "nounset", \
    "-o", "verbose", \
    "-o", "errtrace", \
    "-O", "inherit_errexit", \
    "-O", "shift_verbose", \
    "-c" \
]
env TZ='Etc/UTC'
env LANG='en_US.UTF-8'

arg DEBIAN_FRONTEND=noninteractive

# Latch SDK
# DO NOT REMOVE
run pip install "latch[nextflow]"==2.40.4.dev3
run mkdir /opt/latch
run apt-get update && apt-get install -y default-jre-headless

# Copy workflow data (use .dockerignore to skip files)
copy . /root/


# Latch nextflow workflow entrypoint
# DO NOT CHANGE

copy .latch/bin/nextflow /root/nextflow
copy .latch/.nextflow /root/.nextflow
copy .latch/nf_entrypoint.py /root/nf_entrypoint.py

# Latch workflow registration metadata
# DO NOT CHANGE
arg tag
# DO NOT CHANGE
env FLYTE_INTERNAL_IMAGE $tag

workdir /root
