# Nginx Alpine SSL

This will create a basic nginx ssl enabled http server that runs on alpine.

## Requirements

- Docker CE

## Options

`-e CRT={your-cert-name.crt}` - allows you to specify your own `crt` file  (note there is a default for mydomain.com).

`-e KEY={your-private-key.key}` - allows you to specify your own `key` file (note there is a default for mydomain.com).

## Generate Your Own Self-Signed SSL

```bash
docker run --rm -v $PWD/local/path:/usr/share alpine /bin/sh -c "apk add openssl; openssl req -x509 -nodes -days 365 -subj \"/C=CA/ST=QC/O=Company, Inc./CN=yourdomain.com\" -addext \"subjectAltName=DNS:yourdomain.com\" -newkey rsa:2048 -keyout /usr/share/your-key-name.key -out /usr/share/your-cert-name.crt;"
```

## Example Run

```bash
docker run -it -d -v $PWD/local/path:/etc/ssl/private/ -v $PWD/local/path:/etc/ssl/certs/ -e CRT=your-cert-name.crt -e KEY=your-private-key.key -p 80:80 -p 443:443 --name container-name {docker-hub-user}/{docker-hub-repo};
```
