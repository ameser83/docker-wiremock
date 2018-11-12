# Introduction 
This project contains the source files and example implementation for Docker WireMock Container

# Content
1.  Overview of Docker Containers
       + What is a Docker Container?
            + [Docker Container](https://www.docker.com/resources/what-container)
       + What is a Dockerfile?
            + [Dockerfile](https://docs.docker.com/engine/reference/builder)
       + What is a Docker Compose file?
            + [Docker Compose File](https://docs.docker.com/compose/compose-file)

2.  Overview of WireMock
       + What is WireMock?
            + [WireMock](http://wiremock.org/)
       + WireMock Documentation
            + [Docs](http://wiremock.org/docs/)


# Getting Started
1. Installation process
    +  Download Docker Desktop Installer
        + [Docker Desktop](https://www.docker.com/products/docker-desktop)
        +  Follow the standard instructions from the wizard.

2. Clone git repo from vsts
    +  [docker-wiremock](https://github.com/ameser83/docker-wiremock)

    + How to run the example project
        1. Open PowerShell
        
        2. Navigate to the solution folder
            ```
            PS > cd /yourRepoFolder/docker-wiremock
            ```
        3. Execute compose command
            ```
            PS > docker-compose up --build
            ```
        4. Results
            ```
            PS > docker-compose up --build
            Building wiremock
            Step 1/9 : FROM anapsix/alpine-java:8
            8: Pulling from anapsix/alpine-java
            4fe2ade4980c: Pull complete
            051d64e46a28: Pull complete
            Digest: sha256:35aeae1208d439998b59653e83c8669cfb468001b260e71acb3b2fc970bbf22c
            Status: Downloaded newer image for anapsix/alpine-java:8
            ---> 70cf92036541
            Step 2/9 : RUN apk add --update curl &&     rm -rf /var/cache/apk/*
            ---> Running in c2160184f57e
            fetch http://dl-cdn.alpinelinux.org/alpine/v3.8/main/x86_64/APKINDEX.tar.gz
            fetch http://dl-cdn.alpinelinux.org/alpine/v3.8/community/x86_64/APKINDEX.tar.gz
            (1/4) Installing nghttp2-libs (1.32.0-r0)
            (2/4) Installing libssh2 (1.8.0-r3)
            (3/4) Installing libcurl (7.61.1-r1)
            (4/4) Installing curl (7.61.1-r1)
            Executing busybox-1.28.4-r1.trigger
            Executing glibc-bin-2.28-r0.trigger
            OK: 25 MiB in 32 packages
            Removing intermediate container c2160184f57e
            ---> 4c518079adc2
            Step 3/9 : ENV WM_PACKAGE wiremock
            ---> Running in fc6fd6971867
            Removing intermediate container fc6fd6971867
            ---> 7f5896758f1d
            Step 4/9 : ARG WM_VERSION=2.7.1
            ---> Running in 78214278acce
            Removing intermediate container 78214278acce
            ---> a5f9bdb7f5fb
            Step 5/9 : RUN mkdir /$WM_PACKAGE
            ---> Running in e3b408c004c0
            Removing intermediate container e3b408c004c0
            ---> 085af7bd0528
            Step 6/9 : WORKDIR /$WM_PACKAGE
            ---> Running in 463d28d0b63b
            Removing intermediate container 463d28d0b63b
            ---> db61ea01ff62
            Step 7/9 : RUN curl -sSL -o $WM_PACKAGE.jar https://repo1.maven.org/maven2/com/github/tomakehurst/$WM_PACKAGE-standalone/$WM_VERSION/$WM_PACKAGE-standalone-$WM_VERSION.jar
            ---> Running in af02129092de
            Removing intermediate container af02129092de
            ---> 0839855770fe
            Step 8/9 : EXPOSE 9001
            ---> Running in 1edc0eca0eb2
            Removing intermediate container 1edc0eca0eb2
            ---> f3b586fb6230
            Step 9/9 : ENTRYPOINT ["java","-jar","wiremock.jar","--port","9001","--verbose","--global-response-templating","--enable-browser-proxying"]
            ---> Running in 659e6203c7b9
            Removing intermediate container 659e6203c7b9
            ---> 81e5d9fc8360

            Successfully built 81e5d9fc8360
            Successfully tagged docker-wiremock_wiremock:latest
            Creating docker-wiremock_wiremock_1 ... done
            Attaching to docker-wiremock_wiremock_1
            wiremock_1  | 2018-11-12 18:59:31.581 Verbose logging enabled
            wiremock_1  | SLF4J: Failed to load class "org.slf4j.impl.StaticLoggerBinder".
            wiremock_1  | SLF4J: Defaulting to no-operation (NOP) logger implementation
            wiremock_1  | SLF4J: See http://www.slf4j.org/codes.html#StaticLoggerBinder for further details.
            wiremock_1  | 2018-11-12 18:59:32.539 Verbose logging enabled
            wiremock_1  |  /$$      /$$ /$$                     /$$      /$$                     /$$
            wiremock_1  | | $$  /$ | $$|__/                    | $$$    /$$$                    | $$
            wiremock_1  | | $$ /$$$| $$ /$$  /$$$$$$   /$$$$$$ | $$$$  /$$$$  /$$$$$$   /$$$$$$$| $$   /$$
            wiremock_1  | | $$/$$ $$ $$| $$ /$$__  $$ /$$__  $$| $$ $$/$$ $$ /$$__  $$ /$$_____/| $$  /$$/
            wiremock_1  | | $$$$_  $$$$| $$| $$  \__/| $$$$$$$$| $$  $$$| $$| $$  \ $$| $$      | $$$$$$/
            wiremock_1  | | $$$/ \  $$$| $$| $$      | $$_____/| $$\  $ | $$| $$  | $$| $$      | $$_  $$
            wiremock_1  | | $$/   \  $$| $$| $$      |  $$$$$$$| $$ \/  | $$|  $$$$$$/|  $$$$$$$| $$ \  $$
            wiremock_1  | |__/     \__/|__/|__/       \_______/|__/     |__/ \______/  \_______/|__/  \__/
            wiremock_1  |
            wiremock_1  | port:                         9001
            wiremock_1  | enable-browser-proxying:      true
            wiremock_1  | no-request-journal:           false
            wiremock_1  | verbose:                      true   
            ```
        5. Test the wiremock container with following URL 
        ```
        http://localhost:9001/DemoService/v1/GetData?Id=1

        Response:

        {
            "Name": "Test Name",
            "Age" : 32,
            "Address" : "Test Adress",
            "Active" : true
        }
        ```

# Solution Template

+ Docker WireMock Container Template
    + Solution structure
        ```

            ├── docker-wiremock                              # Solution folder
            ├── __files                                      # Folder containing all response services
            │   ├── DemoServiceResponse                      # Folder containing API calls response data for the demo service
            │       ├── DemoServiceGetData_response.json     # Json get data service response example
            ├── mappings                                     # Folder containing services mapping request with response files
            │   ├── DemoService                              # Contains the mappings for demo service
            │       ├── DemoServiceGetData.json              # Request and response API call mappings.
            ├── docker-compose.yml                           # Docker compose file
            ├── Dockerfile                                   # Dockerfile   
           

        ```
    + Dockerfile script     
        ```
            # --- WIREMOCK --
            FROM anapsix/alpine-java:8

            RUN apk add --update curl && \
            rm -rf /var/cache/apk/*

            ENV WM_PACKAGE wiremock
            ARG WM_VERSION=2.7.1

            RUN mkdir /$WM_PACKAGE
            WORKDIR /$WM_PACKAGE

            RUN curl -sSL -o $WM_PACKAGE.jar https://repo1.maven.org/maven2/com/github/tomakehurst/$WM_PACKAGE-standalone/$WM_VERSION/$WM_PACKAGE-standalone-$WM_VERSION.jar

            EXPOSE 9001

            ENTRYPOINT ["java","-jar","wiremock.jar","--port","9001","--verbose","--global-response-templating","--enable-browser-proxying"]
        ```
    + docker-compose.yml content
        ```
        version: '3.7'

        networks:
        wiremock_net:
        ipam:
            config:
            - subnet: 172.20.0.0/24
            
        services:

        wiremock:

        build:
            context: ./
            dockerfile: Dockerfile
            
        networks:
            wiremock_net:
            ipv4_address: 172.20.0.6
        ports:
            - "9001:9001"
        volumes:
            #we copy our scripts onto the container
            - ./__files:/wiremock/__files
            - ./mappings:/wiremock/mappings
        ```
    + mappings\DemoService\DemoServiceGetData.json (Demo mapping)
        ```
        {
            "request": {
                "method": "GET",
                "urlPathPattern": "/DemoService/v1/GetData",
                "queryParameters": {
                    "Id": {
                        "matches": "[0-9]+"
                    }
                }    
            },
            "response": {
                "status": 200,
                "bodyFileName": "../__files/DemoServiceResponse/DemoServiceGetData_response.json"
            }
        }
        ```

     + __files\DemoServiceResponse\DemoServiceGetData_response.json (Demo response)
        ```
        {
            "Name": "Test Name",
            "Age" : 32,
            "Address" : "Test Adress",
            "Active" : true
        }
        ```
    
# Additional Resources
+ Useful docker commands
    + List all images in local machine
        ```
            > docker images
        ```
    + List all containers in local machine
        ```
            > docker ps -a
        ```
    + Remove docker container 
        ```
            > docker rm [container name or id]
        ```
    + Remove docker image 
        ```
            > docker rmi [image name or id]
        ```
    + Open a container 
        ```
            > docker exec -it [container name or id] [powershell or bash param]
        ```
    + Stop a container 
        ```
            > docker stop [container name or id]
        ```
    + Stop a container 
        ```
            > docker stop [container name or id]
        ```
    + Start a container 
        ```
            > docker container start [container name or id]
        ```
        
