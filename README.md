# Alloy-AutoDiscover

## URL > https://gitlab.prd.dsg-internal/global-linux-team/ansible/roles/descartes.alloy#

## HTTPD / APACHE
Load Mod_status
```bash
cat <<'EOF' > /etc/httpd/conf.d/server-status.conf
LoadModule status_module modules/mod_status.so

ExtendedStatus On

<Location "/server-status">
    SetHandler server-status
    Require ip 127.0.0.1
    Require host galldeglttst17.prd.dsg-internal
</Location>
EOF
systemctl restart httpd
```
## MongoDB configure user and login
add this on mongo.alloy
```bash
//mongodb_uri = "mongodb://metrics:YOUR_PASSWORD@HOSTNAME.prd.dsg-internal:27017/admin"
```
full config
```bash
prometheus.exporter.mongodb "mongodb" {
  mongodb_uri = "mongodb://galldeglttst17.prd.dsg-internal:27017"
//Enable authentication
//mongodb_uri = "mongodb://metrics:YOUR_PASSWORD@HOSTNAME.prd.dsg-internal:27017/admin"
}

prometheus.scrape "mongodb" {
  targets    = prometheus.exporter.mongodb.mongodb.targets
  forward_to = [ prometheus.remote_write.alloy_proxy.receiver ]
}
```
## Nginx enable Nginx Status > /etc/nginx/conf.d/nginx_status.conf
```bash
server {
    listen 80;
    server_name galldeglttst17.prd.dsg-internal;

    location /nginx_status {
        stub_status;
        allow 127.0.0.1;
        allow 10.42.2.56;
        deny all;
    }
}
```
## Squid Add to /etc/squid/squid.conf: and restart systemctl restart squid

```bash
acl prometheus src 127.0.0.1
http_access allow manager prometheus
http_access deny manager
```
## Kafka, for full metrics add to kafka-env.sh and restart kafka
```bash
export JMX_PORT=9999
export KAFKA_JMX_OPTS="-Dcom.sun.management.jmxremote \
                       -Dcom.sun.management.jmxremote.authenticate=false \
                       -Dcom.sun.management.jmxremote.ssl=false"
```

```bash
```

```bash
```

```bash
```

```bash
```

```bash
```

```bash
```

```bash
```


```bash
```

```bash
```
```bash
```

```bash
```
