## Gerenciamento de Projetos com Redmine

### Introdução

De acordo com [site oficial](https://www.redmine.org/), Redmine é um aplicativo open source da Web de gerenciamento de projetos flexível. Escrito usando o framework Ruby on Rails, é multi-plataforma e cross-database.

### Principais Características

---

### Instalando o Redmine

A instalação do Redmine pode ser via:  i) instalador, ii) com Docker ou iii) manualmente.

Neste manual, a instalação será através do Docker Composer e utilizando o SGBD MySQL, mas, o Redmine também integra com outros bancos. Caso ainda não tenha o Docker instalado, acesse o site oficial [https://www.docker.com/](https://www.docker.com/), faça o download de acordo com o Sistema Operacional da sua máquina.

```docker
docker version
```

Instalado o Docker e com o mesmo em iniciado, vamos criar nosso ambiente.

Acesse o [Docker Hub](https://hub.docker.com/_/redmine) e baixe a imagem Redmine.

**Exemplo com docker stack deploy:** Crie um repositório, no arquivo .yml defina os serviços com a infraestrutura desejada.

[stack.yml](https://github.com/PriCampos/config-redmine/blob/master/stack.yml) 

```yaml
version: '3.1'

services:

  redmine:
    image: redmine
    restart: always
    ports:
      - 80:3000
    environment:
      REDMINE_DB_MYSQL: db
      REDMINE_DB_PASSWORD: priscila
      REDMINE_DB_DATABASE: priscila

  db:
    image: mysql:5.7
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: priscila
      MYSQL_DATABASE: priscila
```

**(lembre de alterar a senha e o nome da base de dados)**

No repositório onde foi criado o arquivo Docker Compose, execute:

```docker-compose
docker-compose -f stack.yml up
```

Verifique se os serviços foram iniciados (na primeira vez, esse processo vai demorar um pouco).

```docker
docker ps
```

![print do terminal mostrando as imagens do docker iniciadas](https://raw.githubusercontent.com/PriCampos/config-redmine/master/images/imagens-docker.png)


Iniciados, acesse o servidor da aplicação, neste caso, a própria máquina apontando para porta definida no stack.yml [http://localhost:8080/](http://localhost:8080/).













