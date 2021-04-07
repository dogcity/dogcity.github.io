# Implementar sitio web estático en AWS con HTTPS (S3, Route 53, CloudFront, Certificate Manager)

## Esquema
![Diagrama web en S3](https://i.imgur.com/mhmVtfS.png)

## Pre Requisitos
- Dominio
- Proyecto web
- Cuenta Amazon AWS

## Proceso
1. Ingresar a AWS
2. Ingresar a S3
3. Crear bucket con nombre único o del dominio
	3.1. Click en botón  "Crear bucket"
	3.2. Ingresar nombre del bucket "example-bucket"
	3.3. Desmarcar la opción "Bloquear  _todo_  el acceso público"
	3.4. Marcar la opción para aceptar el acceso público "Reconozco que la configuración actual puede provocar que este bucket y los objetos que contiene se vuelvan públicos."
	3.5. Agregar etiqueta para realizar búsquedas, análisis o visualizar el detalle en factura de ser necesario
	- Clave: Name
	- Valor: Nombre del bucket
	3.6. Click en botón "Crear bucket"
4. Subir proyecto a bucket S3
	4.1. Ingresar al bucket creado
	4.2. Ingresar en Objetos
	4.3. Arrastrar archivos del proyecto aquí
	4.4. Click en botón "Cargar"
5. Dar acceso publico
	5.1. Ingresar al bucket creado
	5.2. Ingresar en Permisos
	5.3. Ir a apartado "Política de bucket"
	5.4. Click en botón "Editar"
	5.5. En campo de texto ingresar la siguiente política
	```
	{
		"Version": "2012-10-17",
		"Statement": [{
			"Sid": "AllowPublicReadAccess",
			"Effect": "Allow",
			"Principal": "*",
			"Action": ["s3:GetObject"],
			"Resource": ["arn:aws:s3:::example-bucket/*"]
		}]
	}
	```
	5.6. Modificar "example-bucket" por el nombre del bucket
	5.7. Click en "Guardar cambios"
6. Habilitar bucket como sitio web
	6.1. Ingresar en Propiedades
	6.2. Ir a apartado "Alojamiento de sitios web estáticos"
	6.3. Click en botón "Editar"
	6.4. Seleccionar opción "Habilitar"
	6.5. Seleccionar opción "Alojar un sitio web estático"
	6.6. En "Documento de índice" ingresar "index.html"
	6.7. En "Documento de error _-  opcional_" ingresar "index.html"
	6.8. Click en botón "Guardar cambios"
	6.9. Ir a apartado "Alojamiento de sitios web estáticos"
	6.10. Hacer click en url "http://example-bucket.s3-website-us-east-1.amazonaws.com/"
> Hasta aquí ya tenemos publicado el proyecto web a un nivel básico sin certificado SSL
7. Registrar Dominio en Route 53
8. Crear Certificado SSL
	8.1. Ingresar a Certificate Manager
	8.2. Click en botón "Solicitar un certificado"
	8.3. Seleccionar "Solicitar un certificado público"
	8.4. Click en botón "Solicitar un certificado"
	8.5. Agregar nombre de dominio "mi-dominio.com"
	8.6. Click en botón "Agregar otro nombre a este certificado"
	8.7. Agregar nombre de dominio con comodín para que cualquier subdominio que se cree posteriormente quede cubierto "*.mi-dominio.com"
	8.8. Click en botón "Siguiente"
	8.9. Seleccionar "Validación de DNS"
	8.10. Click en botón "Siguiente"
	8.11. Agregar etiqueta
	- Nombre de la etiqueta: Name
	- Valor: SSL mi-dominio.com con comodín
	8.12. Click botón "Revisar"
	8.13. Click botón "Confirmar y solicitar"
> Esperar que el estado cambie a "Emitido"
9. Configuración e implementar todo lo realizado en CloudFront
	9.1. Ingresar en CloudFront
	9.2. Click en botón "Create Distribution"
	9.3. Ir a apartado Web
	9.4. Click en botón "Get Started"
	9.5. Apartado "Origin Settings"
		9.5.1. Origin Domain Name: Seleccionar el bucket creado para el proyecto "example-bucket.s3.amazonaws.com"
	9.6. Apartado "Default Cache Behavior Settings"
		9.6.1. Viewer Protocol Policy: Seleccionar redirección HTTPS "Redirect HTTP to HTTPS"
	9.7. Apartado "### Distribution Settings"
		9.7.1. Alternate Domain Names (CNAMEs): Ingresar la url que desea o ingresará en Route 53, dominio y/o subdominio completo
		9.7.2. SSL Certificate: Seleccionar certificado propio "Custom SSL Certificate (example.com)"
		9.7.3. En input que se habilita seleccionar el certificado SSL creado arriba
	9.8. Click en botón "Create Distribution"
> Esto puede tardar hasta 1 hora
10. Enlazar proyecto al DNS, Route 53
	10.1. Ingresar a Route 53
	10.2. Ingresar a la Zona creada
	10.3. Ingresar al dominio correspondiente
	10.4. Click en botón "Crear un registro"
		10.4.1. Nombre del registro: Dejar en blanco si apunta al dominio, de ser un subdominio ingresarlo
		10.4.2. Tipo de registro: Dejar por defecto "A"
		10.4.3. Alias: Activar
		10.4.4. Dirigir el tráfico a: Seleccionar lo siguiente
		- Alias de la distribución de CloudFront
		- Selecciona tu zona de distribución (EE. UU. Este (Norte de Virginia))
		- Selecciona la distribución CloudFront creada
		10.4.5. Política de direccionamiento: Dejar por defecto
		10.4.6. Evaluar el estado del destino: Dejar por defecto
		10.4.7. Click en botón "Crear registros"
> 10.4.4: Si no visualiza la distribución CloudFront asegúrese de haber ingresado el CNAME correctamente en el punto 9.7.1 y revise que coincida con el Nombre de registro ingresado en el punto 10.4.1
