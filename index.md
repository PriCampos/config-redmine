## Gerenciamento de Projetos com Redmine
---

### Introdução

De acordo com [site oficial](https://www.redmine.org/), Redmine é um aplicativo open source da Web de gerenciamento de projetos flexível. Escrito usando o framework Ruby on Rails, é multi-plataforma e cross-database.

### Principais Características

### Instalando o Redmine

A instalação do Redmine pode ser via:  i) instalador, ii) com Docker ou iii) manualmente.

Neste manual, a instalação será através do Docker e utilizando o SGBD MySQL. Caso não tenha o Docker instalado, acesse o site oficial [https://www.docker.com/](https://www.docker.com/), faça o download de acordo com o Sistema Operacional da sua máquina. ;)

```docker
docker version
```

Instalado o Docker e com o mesmo em execução, vamos criar nosso ambiente.

Acesse o [Docker Hub](https://hub.docker.com/_/redmine) e baixe a imagem Redmine.

Exemplo com docker stack deploy: Crie um repositório, no arquivo .yml defina os serviços com a infraestrutura desejada.

stack.yml

```yaml
version: '3.1'

services:

  redmine:
    image: redmine
    restart: always
    ports:
      - 8080:3000
    environment:
      REDMINE_DB_MYSQL: user_redmine 
      REDMINE_DB_PASSWORD: redmine 

  db:
    image: mysql:5.7
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: db_priscila 
      MYSQL_DATABASE: priscila 
```

No repositóri onde foi criado o arquivo Docker Compose, execute:

```docker-compose
docker-compose -f stack.yml up
```

Com os serviços iniciados, acesse o servidor da aplicação: [http://localhost:8080/](http://localhost:8080/)

```docker
docker ps
```












