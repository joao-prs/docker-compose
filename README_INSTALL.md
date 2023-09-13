# Instalação do Docker
Siga os passos a seguir para construir seu ambiente ubuntu.
```sh
apt update -y

apt install -y docker.io docker-compose

sudo systemctl enable docker
sudo systemctl start docker
```

modifique seu usuário
```sh
usermod -aG docker ubuntu
```
E pronto, já pode usar o seu novo ambiente
> em outras distros, as alterações de instalação serão mínimas.

## Docker Swarm

Criando o cluster swarm, você executará o seguinte comando no nó master:
```sh
docker swarm init --advertise-addr “ip_da_instância”
```
a saída será similar a esta e serve para adicionar outro worker:
```
docker swarm join --token SWMTKN-1-2164xvum9q3v5v5x741qq66c3vp19q39siqy53eaxe1iopijes-61yhjqnxmerejd0mpon6o6u9t 192.168.0.10:2377
```

mas caso queira adicionar outro manager/master, execute este comando:
```sh
docker swarm join-token manager
```
e a saída será similar a esta, mas terá um token diferente do token de worker:
```
docker swarm join --token SWMTKN-1-2164xvum9q3v5v5x741qq66c3vp19q39siqy53eaxe1iopijes-0pm316s21bb0rv7g0fxe6p28o 192.168.0.10:2377
```

Pronto, vocè tem um cluster docker. 😊