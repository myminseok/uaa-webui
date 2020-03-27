
# create uaa admin client
```
# sshing into ospman VM

uaac target https://uaa.system.pcfdemo.net --skip-ssl-validation
uaac token client get admin -s <uaa-admin-client-secret>
uaac client add uaa-admin-client --authorities "zones.read clients.read clients.secret clients.write uaa.admin clients.admin scim.write scim.read" --authorized_grant_types=password,client_credentials
uaac secret set uaa-admin-client -s <uaa-admin-client-secret>
```


# UAA WebUI
[![Go Report Card](https://goreportcard.com/badge/github.com/shreddedbacon/uaa-webui)](https://goreportcard.com/report/github.com/shreddedbacon/uaa-webui)

This is intended to be a quick web interface for UAA to perform basic functionality via the browser.

# Docker
## Docker Compose
Modify .envvars to suit the target UAA then run one of the following
```
docker-compose up -d
## OR to rebuild
docker-compose up -d --build
```

## Build
```
docker build -t shreddedbacon/uaa-webui .
```
## Run
```
docker run -p 8443:8443 \
  -e CLIENT_ID=uaa-admin \
  -e CLIENT_SECRET=uaa-adminsecret \
  -e UI_URL=https://localhost:8443 \
  -e UAA_SERVER=https://<ip>:<port> \
  shreddedbacon/uaa-webui
```
E.g
```
docker run -p 8443:8443 \
  -e CLIENT_ID=uaa-admin \
  -e CLIENT_SECRET=uaa-adminsecret \
  -e UI_URL=https://localhost:8444 \
  -e UAA_SERVER=https://192.168.50.6:8443 \
  shreddedbacon/uaa-webui
```
