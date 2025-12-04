# Alloy-AutoDiscover


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

```bash
```
```bash
```

```bash
```
