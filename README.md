# Pila-LAMP
>*Realizado por José Manuel Martín Jaén*
>##ÍNDICE
  1. [Introducción](#introducción)
  2. [Configuración base](#configuración-base)
  3. [Configuración Apache y PHP](#configuración-apache-y-php)
  4. [Configuración de MariaDB](#configuración-de-mariadb)
  5. [Comprobación de funcionamiento](#comprobación-de-funcionamiento)
  6. [Conclusión](#conclusión)
>## Introducción: 
>**En este Readme se podrá observar los pasos a realizar para crear una infraestructura de dos niveles con apache y MariaDB.**
## Configuración base
+ Configuración de vagrantfile.
>*Este es el contenido que debemos tener en nuestro archivo para que todo se configure correctamente:*
>![image](https://github.com/jmmartinj02/Pila-LAMP/assets/146434706/26829eee-100d-4f2a-9628-55b95a3c176f)
+ Estos son los scripts que usaremos para que ambas máquinas estén listas al iniciarlas.
>*Script de la máquina Apache:*
>
>![image](https://github.com/jmmartinj02/Pila-LAMP/assets/146434706/ff60dc89-477e-41cd-be2b-d3c57bc11fd4)
>
>*Script de la máquina MariaDB:*  
>![image](https://github.com/jmmartinj02/Pila-LAMP/assets/146434706/58fee5f8-b14b-458e-8619-58878df11c9c)
## Configuración Apache y PHP
+ Despues de inciar las máquinas con vagrant up y de hacer un vagrant provision, iniciamos la maquina de apache con vagrant ssh JoseMMartApache, donde creamos y modificamos el archivo info.php en el directorio /var/www/html.
>*Aquí se puede observar el contenido del archivo*
>![image](https://github.com/jmmartinj02/Pila-LAMP/assets/146434706/0fa43350-3222-442c-8330-e6ad34c1e7f2)
+ Comprobamos desde nuestro navegador que podemos acceder al archivo, utilizando la ip de la máquina que tiene apache:
>*Se puede observar en la barra de navegación qué es necesario escribir.*
>![image](https://github.com/jmmartinj02/Pila-LAMP/assets/146434706/d821f401-558b-407e-a94a-ef583ac7bdc9)
+ Realizamos una clonación de los archivos de los repositorios remotos a la máquina Apache con este comando y le cambiamos el nombre a uno mas sencillo:
>*Se puede observar en qué directorio debemos realizar la clonación y el nombre que le damos.*
>![image](https://github.com/jmmartinj02/Pila-LAMP/assets/146434706/edde7382-b53e-416a-98ac-5fa7d562bda8)
![image](https://github.com/jmmartinj02/Pila-LAMP/assets/146434706/9e8fbc0b-8f3b-49c8-bee4-917d823024d3)
+ Modificamos en la máquina de Apache el archivo config.php del directorio /var/www/html/LAMP/src
>*Introducimos el nombre de la base datos, usuario, contraseña que crearemos mas adelante y la dirección IP de la máquina con Mariadb.
>![image](https://github.com/jmmartinj02/Pila-LAMP/assets/146434706/71a1cd4e-9f45-4aef-9648-838076ea11d3)
+ A continuación nos dirigimos al directorio /etc/apache2/sites-available y editamos el archivo 000-default.conf, añadimos el directorio clonado y su subdirectorio src en DocumentRoot:
>*Añadimos a DocumentRoot LAMP/src*
>![image](https://github.com/jmmartinj02/Pila-LAMP/assets/146434706/a590e9d5-e334-45ea-b6c2-1e2b167861a5)
>![image](https://github.com/jmmartinj02/Pila-LAMP/assets/146434706/6940464d-92f7-4ea3-b660-d2636fb64ade)
## Configuración de MariaDB
+ Cambiamos de máquina y modificamos el archivo en el que se especifica a que servidor debe "enlazarse" el cliente, donde colocaremos la IP de nuestra máquina que tiene MariaDB.
>*El archivo se encuentra en /etc/mysql/mariadb.conf.d .La IP de la máquina que tiene MariaDB en nuestro caso es: 172.16.2.15*
>![image](https://github.com/jmmartinj02/Pila-LAMP/assets/146434706/a5b75ee4-e365-4beb-9bf5-a5d62069fd99)
>![image](https://github.com/jmmartinj02/Pila-LAMP/assets/146434706/c7f07ad9-e183-4d7a-8061-bc9d40f9300b)
+ Creamos el usuario entrando en mysql como root y proporcionamos permisos:
>*Le colocamos al usuario la IP de la máquina con Mariadb, porque será hacia ella con la que accederemos de forma remota.*
>![image](https://github.com/jmmartinj02/Pila-LAMP/assets/146434706/953cfba4-1ec8-4bd7-a6eb-1a30a4fefdfa)
>![image](https://github.com/jmmartinj02/Pila-LAMP/assets/146434706/d3cac8fc-216a-44ab-8e34-a6b0642e83ca)
+ Creamos la base de datos que se encuentra en la carpeta compartida:
>![image](https://github.com/jmmartinj02/Pila-LAMP/assets/146434706/ed039ded-b2e3-45da-aa34-d3ac4422970e)
## Comprobación de funcionamiento
+ Volvemos a la máquina de Apache e iniciamos sesión con el usuario creado anteriormente en mysql usando la IP de la máquina con Mysql y accedemos a la base de datos.
>![image](https://github.com/jmmartinj02/Pila-LAMP/assets/146434706/27f253a1-363b-4e83-bede-a5be3fb99951)
+ Finalmente con la IP con la que estamos ejecutando ambas máquinas, en mi caso 192.168.137.118 y el puerto que hemos configurado en el vagrantfile al principio.
>*En la barra de busqueda tendríamos que poner algo tal que así http://192.168.137.118:8080*
>![image](https://github.com/jmmartinj02/Pila-LAMP/assets/146434706/3e58fbcd-1d7b-4cc2-bbd4-2cac45d43701)
+ Para comprobar que todo se ha hecho correctamente introducimos información en la base de datos.
>![image](https://github.com/jmmartinj02/Pila-LAMP/assets/146434706/2f5bf630-c1b2-4090-94d1-b860168ebc39)
>![image](https://github.com/jmmartinj02/Pila-LAMP/assets/146434706/4f74adb4-bdd8-4428-87b9-aa6ce80d0258)
## Conclusión
+ He de decir, que ha sido un quebradero de cabeza, no es muy difícil esta práctica, pero el problema reside en mi impaciencia al sufrir algún fallo, ya que al hacer algún vagrant reload he terminado el proceso antes de que acabara, provocando que la máquina se volviese inservible, teniendo que hacer configuraciones desde cero, no ha sido un reto muy complicado, creo que debería de tomarme las cosas con más calma y pensar un poco más antes de actuar.
