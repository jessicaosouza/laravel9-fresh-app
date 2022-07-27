# Frash app laravel

Aplicação limpa para desenvolvimento livre utilizando Laravel 9 com Jetstream Inertia, utiliza o laravel mix para compilar os assets ao invés do vite. Contém também um Dockerfile configurado para trabalhar com PHP v8.1, NodeJS v18.6.0, versão atual do Composer, versão atual do Nginx, Mysql v8 e Php MyAdmin. Stacks configuradas em containers, integradas pelo arquivo docker-compose.yml.


## Configuração

```bash
# Clonar o repositório
$ git clone git@github.com:jessicaosouza/laravel9-fresh-app.git

# Entrar na pasta do repositório clonado
$ cd laravel9-fresh-app

# Subir o container do docker
$ docker-compose up -d

# Instalar dependencias do projeto 
$ docker-compose exec app composer install
$ docker-compose exec app npm install

# Criar o arquivo de variáveis ambiente
$ cp .env.development .env

```
Em seguida, vamos configurar as variáveis de acesso ao banco de dados no arquivo .env com as configurações de conexão disponibilizadas no arquivo docker-compose.yml

```shell
DB_CONNECTION=mysql
DB_HOST=treinamentodb #nome do container (container_name)
DB_PORT=3306
DB_DATABASE=treinamento #MYSQL_DATABASE
DB_USERNAME=user #MYSQL_USER
DB_PASSWORD=root #MYSQL_PASSWORD
```
> ⚠️ Sempre que alterarmos o arquivo .env devemos atualizar o cache do app.

```bash
# Adicionar novas configurações no cache
$ docker-compose exec app php artisan config:cache

# Criar e popular o banco de dados
$ docker-compose exec app php artisan migrate:fresh --seed
```

💡 Usamos o comando docker-compose exec app para executar comandos nos containers, para diminuir o tamanho dos comandos, podemos criar um aliás para `docker-compose exec app`. Segue uma dica de como fazer caso esteja utilizando `oh my zsh`



```bash
# Abrir o arquivo de configuração com seu editor preferido, eu gosto do nano
$ nano ~/.zshrc
```

Ao final do arquivo, criar um alias, chamei meu atalho de `doit`

```shell
alias doit='docker-compose exec app'
```

Após adicionar a linha ao final do arquivo, salvar e fechar. Finalmente, devemos atualizar as configurações do terminal:

```bash
$ source ~/.zshrc
```


## Referencias

Para desenvolver utilizando containers do docker e integrá-los eu segui os vídeos da [Erika Heidi](https://github.com/erikaheidi) ⭐️.


