# DOCKER-COMPOSE-PHP
 ## Descrição
 Modelo de docker-compose para um servidor php. Utilizando php-fpm, nginx, mysql e redis nas seguintes versões:
 - php-fpm 7.4
 - nginx 1.19.3
 - mysql
 - redis

 ## Configurando os containers
 ### NGINX
 Pode-se configurar: 
 1. as portas que serão expostas (http e https):
    -  NGINX_HTTP_PORT=80
    - NGINX_HTTPS_PORT=443
 2. o caminho da aplicação:
    - APPLICATION
 3. o caminho dos arquivos de log:
    - NGINX_LOG_PATH=./nginx/logs/
 4. o caminho dos arquivos de configuração do site:
    - NGINX_CONF_PATH=./nginx/sites/ 
