1. előkészület
- docker desktop fut
- container tools és dev containers telepítve van a vsc-ben

2. backend/Dockerfile

3. frontend/Dockerfile

4. mysql/init.sql

5. docker-compose.yml
- docker-compose.yml
    ```
    services:
      db:
        image: mysql:8.0
        container_name: todo-db
        restart: unless-stopped
        environment:
          MYSQL_DATABASE: todo_db
          MYSQL_USER: todo
          MYSQL_PASSWORD: todo_secret
          MYSQL_ROOT_PASSWORD: root_secret
        ports:
          - "3307:3306"
        volumes:
          - dbdata:/var/lib/mysql
          - ./docker/mysql/init.sql:/docker-entrypoint-initdb.d/init.sql:ro
        healthcheck:
          test: ["CMD", "mysqladmin", "ping", "-h", "localhost", "-proot_secret"]
          interval: 5s
          timeout: 5s
          retries: 20

    adminer:
      image: adminer
      container_name: todo-adminer
      restart: unless-stopped
      ports:
        - "8081:8080"
      depends_on:
        - db

    backend:
      build: ./docker/backend
      container_name: todo-backend
      restart: unless-stopped
      volumes:
        - ./backend:/var/www
      ports:
        - "8001:8000"
      depends_on:
        db:
          condition: service_healthy

    frontend:
      build: ./docker/frontend
      container_name: todo-frontend
      restart: unless-stopped
      volumes:
        - ./frontend:/app
      ports:
        - "5174:5173"
      environment:
        - CHOKIDAR_USEPOLLING=true
      depends_on:
        - backend

        volumes:
          dbdata:
    ```

6. containerek futtatása

7. verzió kezelés
    - git app .; git commit -m "üzenet"; git push

8. Dockerfile-ok
- docker/backend/Dockerfile
    ```
    FROM php:8.3-cli

    RUN apt-get update && apt-get install -y git unzip libzip-dev \
        && docker-php-ext-install pdo_mysql zip \
        && rm -rf /var/li/apt/lists/*

    COPY --from=composer:2 /usr/bin/composer /usr/bin/composer

    WORKDIR /var/www

    EXPOSE 8000

    CMD ["tail", "-f", "/dev/null"]
    ```
- docker/frontend/Dockerfile
    ```
    FROM node:22-alpine

    WORKDIR /a

    EXPOSE 5173

    CMD ["tail", "-f", "/dev/null"]
    ```
- docker/mysql/init.sql
    ```
    CREATE DATABASE IF NOT EXISTS todo_db_test;
    GRANT ALL PRIVILEGES ON todo_db_test.* TO 'todo'@'%';
    FLUSH PRIVILEGES;
    ```

9. container-ek futtatása
 - attach sell: a container menüpontban, jobb klikkel kattintva, új terminál nyílik ahol új parancsot lehet létrehozni 
