# harbor-vuln-data
harbor cve vulnerabilities data for test network disconnection environment

# environment
harbor v2.1.6 with clair

# install
you need run harbor with clair
```console
./install --with-clair
```
stop harbor-db docker
```console
docker stop $(docker ps  |grep harbor-db | awk -F ' ' '{print $1}')
```
load vulnerabilities data 
```console
docker exec -i harbor-db psql -U postgres < clear.sql
docker exec -i harbor-db psql -U postgres < vulnerability.sql
docker run -d -p 80:80 -v /var/run/docker.sock:/tmp/docker.sock:ro nginxproxy/nginx-proxy
```
restart harbor
```console
docker-compose down
docker-compose up -d
```
