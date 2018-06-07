# examen
Examen de calculadora que hace 4 operaciones bàsicas.

Correr vertx desde docker:

1. Descargar docker
docker pull berejoselin/examen

2.Correr docker
Ejecutarlo tantas veces como se desee:
docker run -it -p 808x:8080 -e PBA=examenx berejoselin/examen java -jar sample-1.0-SNAPSHOT-fat.jar

(X corresponde a los distintos puertos donde se va a desplegar de acuerdo al archivo de configuración-backend- de tu HAProxy)

Nota. SE debe elegir un puerto disponible
********************************************************************************************************************************
BALANCEAR EL SERVICIO CON HAPROXY:

//instalar haproxy
sudo apt-get install haproxy
//dentro del documento descomentamos en .cfg y agregamos ENABLED=1
sudo nano /etc/default/haproxy
***************************
//dentro del documento
sudo nano etc/haproxy/haproxy.cfg
//escribimos hasta abajo
frontend www   
    bind localhost:9090
    default_backend site-backend   

    backend site-backend
        mode http
        balance roundrobin
        server lamp1 localhost:8081 check
        server lamp2 localhost:8082 check
        server lamp3 localhost:8083 check
        server lamp4 localhost:8084 check
        server lamp5 localhost:8085 check
        server lamp6 localhost:8086 check

********************************************************
docker run -d -p 8081:80 ngnix
docker run -d -p 8082:80 ngnix
docker run -d -p 8083:80 ngnix
docker run -d -p 8084:80 ngnix
docker run -d -p 8085:80 ngnix
docker run -d -p 8086:80 ngnix

**************************************************************************
Probarlo en: 
http://localhost:XXXX/api/sumar?a=Y&b=Z

http://localhost:XXXX/api/restar?a=Y&b=Z

http://localhost:XXXX/api/multiplica?a=Y&b=Z

http://localhost:XXXX/api/divide?a=Y&b=Z

(donde las XXXX es el numero de puerto del frontend del HAProxy,
Y y Z son los numeros de la operación seleccionada)

