# Docker-Mail
https://github.com/tomav/docker-mailserver </br>
vagrant plugin install vagrant-docker-compose

mkdir /etc/docker-mail </br>
cd /etc/docker-mail </br>
docker pull tvial/docker-mailserver:latest </br>
curl -o setup.sh https://raw.githubusercontent.com/tomav/docker-mailserver/master/setup.sh; chmod a+x ./setup.sh </br>
vi docker-compose.yml </br>
```bash
version: '2'

services:
  mail:
    image: tvial/docker-mailserver:latest
    hostname: mail
    domainname: tandem123.local
    container_name: mail
    ports:
    - "25:25"
    - "143:143"
    volumes:
    - maildata:/var/mail
    - mailstate:/var/mail-state
    - ./config/:/tmp/docker-mailserver/
    environment:
    - ENABLE_SPAMASSASSIN=0
    - ENABLE_CLAMAV=0
    - ENABLE_FAIL2BAN=0
    - ENABLE_POSTGREY=0
    - ONE_DIR=1
    - DMS_DEBUG=0
    cap_add:
    - NET_ADMIN
    - SYS_PTRACE

volumes:
  maildata:
    driver: local
  mailstate:
    driver: local
    ```
    ./setup.sh email add test@tandem123.local
