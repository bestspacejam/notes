# Установка Docker Registry с сертификатом Let's Encrypt

```shell
# За основу взят скрипт:
# https://gist.github.com/PieterScheffers/63e4c2fd5553af8a35101b5e868a811e

# Для начала надо прописать debian-backports в `sources.list`
sudo apt-get install certbot -t stretch-backports
sudo certbot certonly --keep-until-expiring --standalone -d domain.example.com --email neter@mail.ru

line="30 2 * * 1 certbot renew >> /var/log/letsencrypt-renew.log"
(crontab -u root -l; echo "$line" ) | crontab -u root -

# Ограничение доступа к Registry:
# https://docs.docker.com/registry/deploying/#restricting-access
mkdir auth
docker run --entrypoint htpasswd registry:2.7.1 -Bbn login password > auth/htpasswd

docker run -d \
  -p 443:443 \
  --restart=always \
  --name registry \
  -v /etc/letsencrypt:/etc/letsencrypt \
  -v /opt/docker-registry:/var/lib/registry \
  -v "$(pwd)"/auth:/auth \
  -e REGISTRY_HTTP_ADDR=0.0.0.0:443 \
  -e REGISTRY_HTTP_TLS_CERTIFICATE=/etc/letsencrypt/live/domain.example.com/fullchain.pem \
  -e REGISTRY_HTTP_TLS_KEY=/etc/letsencrypt/live/domain.example.com/privkey.pem \
  -e "REGISTRY_AUTH=htpasswd" \
  -e "REGISTRY_AUTH_HTPASSWD_REALM=Registry Realm" \
  -e REGISTRY_AUTH_HTPASSWD_PATH=/auth/htpasswd \
  registry:2.7.1

# Просмотр каталога образов:
# https://domain.example.com/v2/_catalog
```
