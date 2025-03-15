# Infrastructure as a Code

Infrastructure as a Code

## Namespaces

`namespaces.yaml`

```yaml
apiVersion: v1
kind: Namespace
metadata:
  name: haapsalu
---
apiVersion: v1
kind: Namespace
metadata:
  name: tallinn
---
apiVersion: v1
kind: Namespace
metadata:
  name: logging
```

## Configmap

`configmap.yaml`

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: todo-config
  namespace: haapsalu
data:
  COMPANY_NAME: "Haapsalu"
  PORT: "8081"
---
apiVersion: v1
kind: ConfigMap
metadata:
  name: todo-config
  namespace: tallinn
data:
  COMPANY_NAME: "Tallinn"
  PORT: "8082"
```

## TLS-sertifikaatide loomine

```bash
openssl req -x509 -nodes -days 365 -newkey rsa:2048   -keyout grafana-tls.key -out grafana-tls.crt   -subj "/CN=grafana.local"
```

## Saladuste lisamine

````bash
sudo kubectl create secret docker-registry ghcr-secret   --docker-server=ghcr.io   --docker-username=mrtrvl   --docker-password=ghp_....   --docker-email=email@email.ee

TLS-i lisamine:

```bash
sudo kubectl create secret tls grafana-tls   --cert=grafana-tls.crt --key=grafana-tls.key   -n logging
````
