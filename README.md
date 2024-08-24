# Guía básica para desarrollar con Quarkus

## Configuración de Ambiente de trabajo 

1. Instalar Quarkus CLI 

    ```
    curl -Ls https://sh.jbang.dev | bash -s - trust add https://repo1.maven.org/maven2/io/quarkus/quarkus-cli/
    curl -Ls https://sh.jbang.dev | bash -s - app install --fresh --force quarkus@quarkusio
    ```

2. Crear una Aplicación
    
    ```
    quarkus create app net.vialabs:quarkus-sample \
        --extension='rest'
        cd quarkus-sample
    ```

3. Ejecutar el proyecto

    ```
    quarkus dev
    ```

## Despliegue Docker local

1. Compilar artefactos nativamente
    
    ```
    docker run --rm -v $(pwd):/work -v "$HOME/.m2:/home/quarkus/.m2" -w /work --entrypoint "" \
        quay.io/quarkus/ubi-quarkus-mandrel-builder-image:23.1-java21 \
        ./mvnw clean package -Dnative 
    ```

2. Construir la imagen docker

    ```
        docker build . -f src/main/docker/Dockerfile.native-micro -t quarkus-sample:1.0.0
    ```

3. Ejecutar la imagen docker

    ```
    docker run -p 8080:8080 quarkus-sample:1.0.0
    ```
