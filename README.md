# Migue_DevOps_Clase1
Comandos aprendidos en la primera clase sobre Docker de la Bootcamp de DevOps

1. Hacemos un pull (descargamos) la siguuiente imagen de apache 2.0 del repositorio de docker hub
   > **docker pull httpd:latest**
   
2. Una vez realizado el pull, nos metemos en el directorio de docker y creamos un dockerfile
   > **cd .docker/**     
   > **nano dockerfile**
    
3. Dentro del dockerfile establecemos la conexión con la imagen descargada mediante 
   > **FROM httpd:latest**

4. Una vez la conexión establecida con la imagen, montamos nuestra imagen en local con la imagen descargada, creandole un tag ("imagen") con -t
   > **docker build -t primeraimagen:latest . **
    
    (Si queremos ver el listado del histórico de imágenes creadas y en ejecución usamos "**docker images**")
    
5. Ya estaría creada la imagen y para lanzar el contenedor usamos el comando run para desplegarlo en nuestra máquina
   > **docker run -p 8080:80 primeraimagen:latest**
    
    (*Si no utilizamos la opción -d para levantarlo en modo demonio, o segundo plano, deberemos abrir una nueva terminal para continuar)
    
    (Para ver el registro de contenedores levantados y su estado usamos "**docker ps -a**")
    
6. En el navegador ponemos nuestra ip:8080 y nos abrirá el index.html

6. En nuestro ejercicio hemos modificado un archivo index.html. Para ello creamos un index.html modificado en el directorio de .docker/. Para crear una imagen nueva con los cambios, tenemos que modificamos el dockerfile con el comando COPY, que copiará nuestro index.html modificado a nuestra nueva imagen.
   > **COPY index.html /usr/local/apache2/htdocs/index.html**
    
7. Volvemos a levantar el contenedor de la imagen  nueva y comprobamos en el navegador que nuestro index.html modificado se ha copiado.
    >    **docker build -t segundaimagen:latest .**
    >    **docker run -p 8080:80 segundaimagen:latest**
        
      (*Podemos parar el contenedor con "docker stop <id>)

8. Por último queremos crear un volumen, un archivo compartido con los contenedores que contendrá los archivos persistentes. Para ello creamos el volumen:
   > **docker create volume mivolumen**
    
   (*Para ver el estado del volumen usamos "**docker volume inspect mivolumen***")
    
9. Levantamos el volumen en la imagen para compartirla (tenemos que pasar el contenedor antes, haciendo un stop):
   > **run -v mivolumen:/opt/data -p8080:80 segundaimagen**
    
    (*para inspeccionar los volúmenes que tiene la imagen "**docker inspect segundaimagen**")
    
10. Por último para abrir una terminal de comandos dentro del contanedor:
   > **docker exect -it idcontainer bash**


