FROM ubuntu:latest
EXPOSE 25565/tcp
EXPOSE 19132/udp
SHELL ["/bin/bash", "-c"]

RUN apt-get update && apt-get install -y \
openjdk-17-jre \
curl \
unzip \
dos2unix \
&& rm -rf /var/lib/apt/lists/*

RUN curl -sL https://www.curseforge.com/minecraft/modpacks/all-of-fabric-5/download/3936583 --output /root/aof5.zip
RUN mkdir -p /app
RUN unzip -qo /root/aof5.zip -d /app/
WORKDIR /app/
COPY eula.txt /app/eula.txt
RUN dos2unix /app/startserver.sh
RUN sed -i 's/curl -o/curl -Lo/g' /app/startserver.sh
RUN echo '#!/bin/bash' | cat - startserver.sh > temp && mv temp startserver.sh
# ENTRYPOINT ["/bin/cp", "-R", "/app /mnt/aof5"]
ENTRYPOINT mkdir -p /mnt/aof5; \
    echo "Copying startserver files over"; \
    /bin/cp -R /app/ /mnt/aof5; \
    echo "Finished moving files"; \
    cd /mnt/aof5/app/; \
    echo "Starting startserver.sh\n"; \
    cd /mnt/aof5/app/; \
    /bin/bash startserver.sh; \
    echo "startserver.sh exited! Sleeping infinitely.\n"; \
    sleep infinity
# WORKDIR /mnt/aof5/app/
# CMD echo "Starting startserver.sh\n"; \
#     cd /mnt/aof5/app/; \
#     /bin/bash startserver.sh; \
#     sleep infinity
# CMD echo "sleeping infinity..." && sleep infinity
