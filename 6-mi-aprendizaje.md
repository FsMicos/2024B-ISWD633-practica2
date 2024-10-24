# Resumen sobre Docker

## Mapeo de Puertos
1. **Especificación de Puertos**: 
   - Al crear un contenedor, se puede mapear un puerto específico del host a un puerto del contenedor con el comando: 
     ```bash
     docker run -d --name <nombre contenedor> --publish published=<valorPuertoHost>,target=<valor> <nombre imagen>:<tag>
     ```
   - Para publicar todos los puertos expuestos de forma automática, se usa:
     ```bash
     docker run -P -d --name <nombre contenedor> <nombre imagen>:<tag>
     ```

2. **Limitaciones**: 
   - No se pueden mapear puertos a un contenedor ya creado; esto debe hacerse al momento de la creación.

3. **Contenedor de Jenkins**: 
   - Se debe crear un contenedor de Jenkins exponiendo los puertos 8080 (interfaz web) y 50000 (comunicación entre nodos).

## Operaciones con Contenedores
1. **Ejecutar Comandos**: 
   - Para ejecutar comandos dentro de un contenedor en ejecución se utiliza:
     ```bash
     docker exec <nombre contenedor> <comando>
     ```
   - Se puede acceder a un shell interactivo usando:
     ```bash
     docker exec -it <nombre contenedor> <shell>
     ```

2. **Ver Logs**: 
   - Para ver los logs de un contenedor, se utiliza:
     ```bash
     docker logs -n <cantidad de líneas> <nombre o id del contenedor>
     ```

## Variables de Entorno
1. **Uso de Variables**: 
   - Las variables de entorno permiten configurar contenedores en diferentes entornos (desarrollo, producción) sin modificar el código.
   - Se pueden establecer variables al crear un contenedor con:
     ```bash
     docker run -d --name <nombre contenedor> -e <nombre variable>=<valor>
     ```

2. **Archivos de Variables**: 
   - También se pueden definir variables en un archivo `.env`, que se puede usar al crear el contenedor con:
     ```bash
     docker run --env-file=<nombreArchivo> <nombre imagen>
     ```

## Redes en Docker
1. **Tipos de Redes**: 
   - **Bridge**: Comunicación entre contenedores en el mismo host.
   - **Host**: Los contenedores comparten la red del host.
   - **None**: Sin configuración de red; los contenedores no pueden comunicarse.

2. **Gestión de Redes**: 
   - Crear una red de tipo bridge:
     ```bash
     docker network create <nombre red> -d bridge
     ```
   - Para conectar o desconectar contenedores a redes, se utilizan:
     ```bash
     docker network connect <nombre red> <nombre contenedor>
     docker network disconnect <nombre red> <nombre contenedor>
     ```

