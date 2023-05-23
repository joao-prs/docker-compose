# compose-passbolt
## About
#### Segurança em primeiro lugar, gerenciador de senhas de código aberto para collaboration
Por fim, um gerenciador de senhas desenvolvido para organizações que levam a segurança e a privacidade a sério. A Passbolt tem a confiança de 15.000 deles em todo o mundo, incluindo empresas F500, indústria de defesa, universidades, startups e muitos outros. 

#### Radical segurança 
Acreditamos que qualquer discussão honesta sobre gerenciadores de senhas deve ser fortemente focada na segurança. A Passbolt coloca a segurança em primeiro lugar. Os principais testadores de penetração avaliam regularmente nosso software e as descobertas são tornadas públicas.

Nosso modelo de segurança oferece suporte a chaves secretas de propriedade do usuário e criptografia de ponta a ponta, mesmo em cenários complexos. A Passbolt está comprometida em praticar a transparência, mantendo as coisas reais e sendo radicalmente aberta. Nós nos recusamos a participar do teatro de segurança. 

#### Construído para colaboração 
Embora a maioria dos gerenciadores de senhas se concentre principalmente em indivíduos. A Passbolt vai um passo além, desenvolvendo uma plataforma que atende às necessidades de organizações e equipes.

Compartilhe suas credenciais com segurança, com ferramentas de auditoria poderosas e confiáveis ​​para usuários avançados. O Passbolt oferece granularidade incomparável para controles de acesso e dados criptografados. 

#### Privacidade em seu DNA 
Com sede na UE🇪🇺, especificamente em Luxemburgo, a privacidade não é apenas uma prioridade; é garantido pela lei.

Não há melhor método para garantir que sua privacidade seja protegida do que hospedá-la atrás de seus firewalls ou em um ambiente sem espaço onde você tenha controle total.

Mesmo as versões pagas do passbolt são 100% open source, permitindo transparência e permitindo que qualquer pessoa audite o código. 

## Modelos de exemplo
#### modelo 1
É utilizado um template geral, ele possui banco de dados.

```yaml
version: '3.4'
services:
  db:
    image: mariadb:10.3
    env_file:
      - env/mysql.env
    volumes:
      - ./database_volume:/var/lib/mysql
    expose:
      - 3306

  passbolt:
    image: passbolt/passbolt:latest-ce
    tty: true
    depends_on:
      - db
    env_file:
      - env/passbolt.env
    volumes:
      - gpg_volume:/etc/passbolt/gpg
      - images_volume:/usr/share/php/passbolt/webroot/img/public
    command: ["/usr/bin/wait-for.sh", "-t", "0", "db:3306", "--", "/docker-entrypoint.sh"]
    ports:
      - 880:80
      - 443:443

volumes:
  gpg_volume:
  images_volume:
```

#### modelo 2
É utilizado servidor de NFS, este já não possui banco de dados. Nota que o servidor de NFS precisa estar configurado, com os diretórios criados e com as devidas permissões para que o passbolt suba.

```yaml
version: '3.7'
volumes:
  gpg_volume: 
    driver: local
    driver_opts:
      type: nfs
      o: nfsvers=4,addr=172.18.32.100,rw
      device: ":/nfs/docker/passbolt-sea/gpg_volume"
  jwt_volume: 
    driver: local
    driver_opts:
      type: nfs
      o: nfsvers=4,addr=172.18.32.100,rw
      device: ":/nfs/docker/passbolt-sea/jwt_volume"

services:
  passbolt:
    #image: passbolt/passbolt:latest-ce
    image: passbolt/passbolt:latest
    env_file:
      - env/passbolt.env
    command: ["/usr/bin/wait-for.sh", "-t", "0", "172.18.32.205:3306", "--", "/docker-entrypoint.sh"]
    ports:
    - 9032:80
    - 9033:443
    tty: true
    volumes:
      - gpg_volume:/etc/passbolt/gpg:rw
      - jwt_volume:/etc/passbolt/jwt:rw
    deploy:
      replicas: 1
      restart_policy:
        condition: on-failure
```