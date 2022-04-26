# Paas con AWS Elastic Beanstalk


## Crear Aplicación

Vamos a crear una aplicación Spring Boot usando Spring Initializr

- Utiliza Spring Initializr

    - Maven
    - Java, versión 11.
    - Group: edu.cc.paas
    - Artifac: holamundo
    - Jar
    - Dependencias: Spring Web y Thymeleaf

- Genera el proyecto y descomprime en tu IDE (AWS Cloud9)

- Comprueba la aplicación de forma local

https://d5fb5be6358943a8922adb524bb8819f.vfs.cloud9.us-east-1.amazonaws.com


## Crear un controlador y una vista

Controlador: Fichero HolaController.java en el directorio src/main/java/edu/cc/paas/holamundo

```
package edu.cc.paas.holamundo;

import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.GetMapping;


@Controller
public class HolaController {
    
    @GetMapping("/")
	public String index() {
	    
		return "index";
	}
    
}
```
Vista: fichero index.html en src/main/resource/templates

```html
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">

    <head>
        <title>Hola Mundo</title>
    </head>
    
    <body>
        <h1>Hola Mundo!!</h1>
	
	</body>
</html>

```

## Construye el proyecto

- Crea el paquete .jar del proyecto

```
./mvnw clean package
```

- Comprueba la aplicación de forma local
 
```
./mvnw spring-boot:run

```

En AWS Cloud9 verás una URl similar a la siguiente con la que podrás acceder a la aplicación:

https://d5fb5be6358943a8922adb524bb8819f.vfs.cloud9.us-east-1.amazonaws.com



## Despliega a producción 

- Cambia el puerto de la aplicación al 5000
AWS Beanstalk utiliza Nginx como servidor web que delegará las peticiones hacía el puerto 5000: por lo que será necesario que nuestra aplicación
utilice dicho puerto. Para ello, en el fichero application.properties incluye la línea

```
server.port=5000
```
Vuelve a construir el proyecto, para generar el fichero .jar.

```
./mvnw clean package
```

El fichero .jar de la aplicación se localiza en el directorio target. Si lo necesitas descarga este fichero a tu equipo local.

- En la consola Web de AWS accede a Elastic Beanstalk

- Crea una Aplicacion

    - Nombre: (el que desees)
    - Plataforma: Java
    - Versión (Ramificación de la plataforma): Corretto 11  (la versión openJDK de amazon)
    - Marca cargar el código, haz clic en el botón "Elegir archivo" y selecciona el fichero .jar descargado en el apartado anterior.
    
- Establece la configuración propia 

    Antes de crear la aplicación, es necesario establecer unas opciones de configuración propias de AWS Academy.
    Para ello, selecciona el botón "Configurar más opciones" y 
        - En seguridad: selecciona
            - Rol de servicio: Rol de servicio
            - Par de claves EC2: vockey
            - Perfil de instancia de IAM: LabInstanceProfile
    Finalmente, pulsa guardar y, en la siguiente ventana, crear aplicación

    Esto creará la aplicación, un entorno Java y un bucket con el fichero .jar de la aplicación.

- Comprueba la app: http://holamundo-env.eba-jpzdcpsd.us-east-1.elasticbeanstalk.com/

    Si todo ha ido bien, podrás acceder a la aplicación en una URL similar a la anterior.