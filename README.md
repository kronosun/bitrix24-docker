! [ Biznet-Bitrix24] (/ docs / assets / bitrix24 - docker - logo . Png )

# Bitrix24 Docker: Web-environment 1C-Bitrix24 Corporate Portal

Allows you to  quickly  and  easily  run  Bitrix24  on  Docker  for  local  development  and  automation of  the  testing process .

## Introduction

Bitrix24  Docker  provides a  ready-made  virtual  environment ,  optimized  for the  development  and  testing  of portal  solutions  Bitriks24 . 

### Use the Bitrix24 Docker if you need to:

- Quickly  deploy a  web  environment  for the  development of  components  and  applications  for  Bitrix24
- get rid from  many  clones of  virtual  machines  for  each  project
- run a clean  copy of the  portal  without  complicated  technical  problems
- Automate running  tests  in the  cloud  ( Continuous  Integration )

## Benefits of this assembly

- Availability specific  for  Bitriks24  services ,  absent  in the  other  assemblies  ( the Push & Pull  server )
- full Compatibility  with  bitrix - the env ,  passing all  built-in  portal tests 
- Base data is  not  included  in the  main  image  and is  connected  via  Docker  Compose
- Opportunity extend  and  connect the  additional  services  ( Import Import phpMyAdmin ,  Codeception  and  so on . d . )
- Using  environment variables  ( to run one container with different parameters )       

## Beginning of work

 We recommend using Docker Compose to work  with  Bitrix24  Docker  .    

Below  is the  configuration  file  `docker-compose.yml`  with  MariaDB connected  , where the launch directory will be mounted on the / local folder inside the container.        
You can change the version of the database or connect several different databases at the same time, supplementing this file with the appropriate instructions.


```yml
version: '3'
services:
  web:
    image: "gcr.io/cloud - management - 265600 / biznet - bitrix : latest "
    ports:
      - " 80 : 80 "
      - " 443 : 443 "
    cap_add:
      - SYS_ADMIN 
    security_opt:
      - seccomp: unconfined
    privileged: true
    volumes:
      - ./:/home/bitrix/www/local
    depends_on:
      - mysql
  mysql:
    image: mariadb
    healthcheck:
      test: " / usr / bin / mysql - user = root - password = + Tr + ( ) 8 ] ! szl [ HQIsoT5 - execute \" SHOW  DATABASES ; \ " "
      interval: 2s
      timeout: 20s
      retries: 10
    ports:
      - " 3306 : 3306"
    environment :
      MYSQL_ROOT_PASSWORD : + Tr + ( ) 8 ]! szl [ HQIsoT5
      MYSQL_DATABASE : sitemanager
      MYSQL_USER : bitrix
      MYSQL_PASSWORD : + Tr + ( ) 8 ]! szl [ HQIsoT5
    command : [ '--character-set-server = utf8' ,  '--collation-server = utf8_unicode_ci' ,  '--skip-character-set-client-handshake' ,  '--sql-mode =' ]   
```

Bitrix24 Docker includes the initial installation files, so after starting the containers, you will immediately see the installation page for a fresh copy of the portal at http: // localhost. 
If you are connecting Bitrix24 Docker to an existing project, change the value to `volumes `sections`web `to` . / : / home / bitrix / www ` . 


### Other startup scripts

-[ Step-by-step  instructions  for  installing the  portal ] (/ docs / 01 - install - step - by - step . Md )
- [ How to  connect  phpMyAdmin ] (/ docs / 02 - phpmyadmin - setup . Md )
- Launch Codeception  tests

## Note

This is  an unofficial  build  and is  intended  exclusively  for  local  development .  Do not  use  this  image  in a  production  environment .
