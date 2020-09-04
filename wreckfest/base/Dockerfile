FROM tianon/wine

# install SteamCMD
RUN set -eux; \
    apt-get update; \
    apt-get install -y --no-install-recommends curl; \
    \
    mkdir /steam; \
    cd /steam; \
    \
    curl -sqL https://steamcdn-a.akamaihd.net/client/installer/steamcmd_linux.tar.gz | tar zxvf -; \
    \
    apt-get remove -y curl; \
    rm -rf /var/lib/apt/lists/*;

# install game
RUN set -eux; \
    cd /steam; \
    \
    mkdir wreckfest; \
    ./steamcmd.sh \
        +login anonymous \
        +@sSteamCmdForcePlatformType windows \
        +force_install_dir ./wreckfest \
        +app_update 361580 \
        +quit; \
    \
    mkdir wreckfest/config;

# setup logs
RUN set -eux; \
    mkdir /steam/wreckfest/logs; \
    ln -s /dev/stdout /steam/wreckfest/logs/server.log;

ADD server_config.cfg /steam/wreckfest/config

ENV DISPLAY=:0
ENV TERM=linux

EXPOSE 27015
EXPOSE 33540/udp
EXPOSE 27016/udp

WORKDIR /steam/wreckfest

CMD wineconsole server/Wreckfest.exe -s server_config=config/server_config.cfg