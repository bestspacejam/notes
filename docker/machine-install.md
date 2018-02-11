# Установка Docker Machine на Linux

Исходная инструкция: [Install Docker Machine](https://docs.docker.com/machine/install-machine/#install-machine-directly)

Скачать и установить Docker Machine:

```shell
curl -L https://github.com/docker/machine/releases/download/v0.13.0/docker-machine-`uname -s`-`uname -m` >/tmp/docker-machine &&
chmod +x /tmp/docker-machine &&
sudo cp /tmp/docker-machine /usr/local/bin/docker-machine
```

Установить дополнение для коммандной строки Bash:

```shell
scripts=( docker-machine-prompt.bash docker-machine-wrapper.bash docker-machine.bash ); for i in "${scripts[@]}"; do sudo wget https://raw.githubusercontent.com/docker/machine/v0.13.0/contrib/completion/bash/${i} -P /etc/bash_completion.d; done
```
