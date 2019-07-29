## Gerenciamento de Projetos com Redmine

---

### Introdução

De acordo com [site oficial](https://www.redmine.org/), Redmine é um aplicativo open source da Web de gerenciamento de projetos flexível. Escrito usando o framework Ruby on Rails, é multi-plataforma e cross-database.

### Principais Características

* Na gestão de usuários é possível verificar: i) período de acesso, ii) bloquear/desbloquear, iii)definir diferentes papéis por projeto, iv) acesso de usuários anônimos ou não cadastrados com permissões específicas v) entre outras preferências de uso pessoal.
* Criar grupos de usuários por projeto atentando a papéis e permissões.
* Personalizar papéis e permissões de forma flexível. Ex: Acesso de gestão de projeto, participar de fóruns visualização de gráficos, repositórios, tipo de tarefas, entre outros.
* Criar tipos de tarefas e associar a fluxo de trabalhos específicos. Ex: Tarefa de Suporte só tem as fases "em andamento e resolvida", mas, tarefas do tipo bug ou funcionalidade precisa das fases "em andamento, code review, testes".
* Criar situação das tarefas. Sendo que, a situação pode ser associada ao commit para análise de progressão do projeto. Ex: Pronta para teste significa 60% de progressão e para isso o Redmine ofece recursos associados ao commit.
* Criar fluxo de trabalho e associá-los a papéis e tipo de tarefas.
* Criar campos personalizados.
* Criar categoria de documentos.
* Criar Prioridade das Tarefas.
* Criar atividades para registro de horas.
* Configuração do Redmine flexivel.
* Uma lista gigante de plugins para impulsionar o uso do Redmine e também a opção de criar os próprios plugins.


---

### Instalando o Redmine

A instalação do Redmine pode ser via:  i) instalador, ii) com Docker ou iii) manualmente.

Neste manual, a instalação será através do Docker Composer e com o SGBD MySQL. Caso ainda não tenha o Docker instalado, acesse o site oficial [https://www.docker.com/](https://www.docker.com/), faça o download de acordo com o Sistema Operacional da sua máquina.

```docker
docker version
```

Finalizada a instalação e iniciado o Docker, vamos criar nosso ambiente.

Acesse o [Docker Hub](https://hub.docker.com/_/redmine) e baixe a imagem Redmine.

**Exemplo com docker stack deploy:** Crie um arquivo .yml no repositório desejado e defina os serviços com a infraestrutura necessária para utilizar o Redmine.

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

Verifique se os serviços foram iniciados:

```docker
docker ps -a
```

![print do terminal mostrando as imagens do docker iniciadas](https://raw.githubusercontent.com/PriCampos/config-redmine/master/images/imagens-docker.png)


Com serviços iniciados, acesse o servidor da aplicação. Neste caso, a própria máquina apontando para porta definida no stack.yml [http://localhost:8080/](http://localhost:8080/).

No dashboard Redmine, clique em Entrar. Atualmente, o usuário e a senha padrão do upstream são admin / admin.

![imagem da tela inicial do Redmine](https://raw.githubusercontent.com/PriCampos/config-redmine/master/images/home-redmine.png)

Em seguida você será direcionado para as etapas de redefinir senha de acesso e alterar os dados da conta.

---

### Configurações Iniciais

Na área logada, clique em Administração > Configurações.

![imagem da tela inicial de configuração geral do projeto](https://raw.githubusercontent.com/PriCampos/config-redmine/master/images/conf-geral-projeto.png)

Na aba geral as modificações particulares de cada projeto são título, texto de boas vindas, nome do servidor e subdomínio e Protocolo.

As parametrizações são bem intuitvas, mas, nessa primeira fase é importante atentar as abas:

* Exibição: onde é importante definir o idioma.

* Autenticação: defina se é permitido ou não o acesso anônimo a projetos públicos e a permissão de auto-login, o sugerido é deixar a opção "sim" para exibição autenticação e "desabilitado" a permissão de autoregistro.

* Arquivos: informe as extensões permitidas ou não nos arquivos do projeto.

![Imagem da configuração de autenticação do projeto](https://raw.githubusercontent.com/PriCampos/config-redmine/master/images/conf-autenticacao-projeto.png)

![Imagem da configuração de arquivo do projeto](https://raw.githubusercontent.com/PriCampos/config-redmine/master/images/conf-arquivo-projeto.png)

### Configurações Avançadas 

As configurações de conexão com o banco de dados, envio de e-mail, entre outras não é realizada via Sistema Redmine, ara alterar é preciso ir direto nos arquivos de modificação do Redmine.

Os principais arquivos estão no diretório htdocs/config no diretório principal do Redmine.

No caso da instalação com Docker...