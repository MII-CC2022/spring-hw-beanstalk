# Paas con AWS Elastic Beanstalk


## Crear Aplicación

Vamos a crear una aplicación Spring Boot usando Spring Initializr

- Utiliza Spring Initializr

-- Maven, Java, versión 11. Group: edu.cc.paas   Artifac: holamundo   Jar
-- Dependencias: Spring Web y Thymeleaf

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

- Comprueba la aplicación de forma local

https://d5fb5be6358943a8922adb524bb8819f.vfs.cloud9.us-east-1.amazonaws.com

## Construye el proyecto

Crea el paquete .jar del proyecto
```
./mvnw clean package
```

## Despliega a producción 


- En la consola Web de AWS accede a Elastic Beanstalk
- Crea una Aplicacion
- Establece la configuración propia 
- Cambia el puerto de la aplicación al 5000
- Comprueba la app: http://holamundo-env.eba-jpzdcpsd.us-east-1.elasticbeanstalk.com/