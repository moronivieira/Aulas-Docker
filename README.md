# Docker Compose
---
<ul>
<li>Install Docker Compose</il>
</ul>

# Preparação 
<ul>
  <li>Criar uma nova pasta para o laboratório:</li>
</ul>
```mkdir lab-11```
```cd lab-11```

# Instruções
<ul>
  <li>Crie um novo arquivo </li>
</ul>

```version: '3.3'

services:
  db:
    image: mysql:26.6.0
    volumes:
    - db_data:/var/lib/mysql
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: somewordpress
      MYSQL_DATABASE: wordpress
      MYSQL_USER: admin
      MYSQL_PASSWORD: wordpress

  wordpress:
    depends_on:
    - db
    image: wordpress:latest
    ports:
    - "8000:80"
    restart: always
    environment:
      WORDPRESS_DB_HOST: db:3306
      WORDPRESS_DB_USER: admin
      WORDPRESS_DB_PASSWORD: wordpress

volumes:
  db_data:

```
<ul>
  <li>Iniciando o contêiner em modo daemon</li>
</ul>

```docker compose up -d ```

<ul>
  <li>Até o container inicializa, inspecione os logs do Wordpress </li>
</ul>

```docker compose logs -f wordpress```

<ul>
  <li>Visualize o container rodando</li>
</ul>

```docker compose ps```

<ul>
  <li>Navegue para o portal WordPress Local</li>
</ul>

```http://<SEU IP>:8000```

<ul>
  <li>Entre no container do MySQL</li>
</ul>


```docker compose exec db bin/bash```

<ul>
  <li>Imprima a variável de ambiente "MYSQL_USER" (configurada dentro do arquivo yaml)</li>
</ul>

```echo $MYSQL_USER```

<ul>
  <li>Saia do container</li>
</ul>

```exit```

<ul>
  <li>Atualize a imagem do mysql no arquivo <b>docker compose</b> para a versão 26.7.0</li>
</ul>

```db:
  image: mysql:26.7.0
  volumes:
  - db_data:/var/lib/mysql
  restart: always
  environment:
    MYSQL_ROOT_PASSWORD: somewordpress
    MYSQL_DATABASE: wordpress
    MYSQL_USER: admin
    MYSQL_PASSWORD: wordpress
```

<ul>
  <il>Limpe o ambiente (remova os contêineres definidos no arquivo docker-compose):</il>
</ul>

```docker-compose down```

<ul>
  <li>Aplique as alterações ao ambiente de execução:</li>
</ul>

```docker-compose up -d```

<ul>
  <il>Observe que os volumes não são excluídos por padrão, então você pode recriar o ambiente a qualquer momento</il>
</ul>

```docker volume ls```
