FROM openjdk:8-jre-stretch

# wget https://ftb.forgecdn.net/FTB2/modpacks/FTBUltimateReloaded/1_7_1/FTBUltimateReloadedServer.zip
# unzip it and place it in directory `extract`

COPY extract /mcserver

WORKDIR /mcserver

RUN   echo eula=true > eula.txt && \
      mkdir /data && \
      sed -i 's|/bin/sh|/bin/bash|g' *.sh && \
      chmod 755 *.sh && \
      ./FTBInstall.sh

# Allow external changes to MAX_RAM by setting KUBE_MAX_RAM
RUN   echo 'export MAX_RAM=${KUBE_MAX_RAM:-$MAX_RAM}' > settings-local.sh

# mcserver creates a bunch of files and directories and
# it's a bit cumbersome to put them on a persistent volume,
# So I thought to copy everything from /mcserver to /data and start it from there.
# it's your responsibility to make that mountpoint persistent

VOLUME ["/data"]

CMD cp -a * /data && cd /data && bash ServerStart.sh
