# BattMo-Server
Jupyterlab Server for [BattMo](https://github.com/BattMoTeam/BattMo)

## Quick start

git clone --recurse-submodules https://github.com/OpenSemanticLab/BattMo-Server
```
cd BattMo-Server
sudo chown -R 1111:1111 data
docker compose build
docker compose up
```
Open ./lab?token=... in your Browser

## Update submodules
```
sudo chown -R "$USER":"$USER" data
git submodule update --init --recursive
sudo chown -R 1111:1111 data
```

## Known problems
### JSON-Handling
octave-docker 7.x leads to the following error:
```
error: jsondecode: support for JSON decoding through RapidJSON was unavailable or disabled when Octave was built
error: called from
    parseBattmoJson at line 4 column 16
    runBattery1D at line 23 column 12
    run at line 78 column 7
```

### Unkown login token
enter the docker container and list running servers
```
docker compose exec -u 0 battmo /bin/bash
jupyter server list
```
if no token is listed, edit the config
```
apt update && apt install nano
nano /etc/jupyter/jupyter_server_config.py
```
set a token with `c.ServerApp.token = '<token>'` and save
```
exit
docker compose stop
docker compose start
```
