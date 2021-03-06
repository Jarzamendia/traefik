# GRPC WEB

Este laboratório tem por objetivo demonstrar como hospedar uma aplicação cliente/servidor com GRPC Web usando o Traefik. Durante os testes preliminares percebemos que na época, o Traefik não conseguia hospedar corretamente aplicações em GRPC Web. Para resolver isto, usamos um proxy Envoy entre o Traefik e o servidor GRPC.

Criamos 5 imagens:

    - jarzamendia/grpc-web-common:grpc-web-lab
    - jarzamendia/grpc-web-client:grpc-web-lab
    - jarzamendia/grpc-web-server:grpc-web-lab
    - jarzamendia/grpc-web-envoy:grpc-web-lab
    - jarzamendia/traefik:grpc-web-lab

- A grpc-web-common hospeda os pre-requisitos para o client e o server.
- O grpc-web-client é um cliente em NodeJS.
- O grpc-web-server é um servidor GRPC em NodeJS, hospedado com um script Pyton.
- O grpc-web-envoy é um proxy envoy, que fará o meio de campo entre o traefik e o GRPC Server.
- O traefik é uma imagem com os certificados necessarios e arquivo de configuração embarcados.



## Urls

    - GRPC Server (Envoy) = frontend.local 
    - GRPC Client = client.local
    - Traefik = traefik.local

Caso você tenha que alterar o endereço do GRPC Server, altera também o cliente....

    - var echoService = new EchoServiceClient('http://frontend.local', null, null);
    - (client\echo\commonjs-example\client.js:26)

Os endereços devem ser apontados para o servidor hospedando o Traefik.

## Ports
    - GRPC Server = 9090
    - ENVOY       = 8080
    - GRPC Client = 8081
    - Traefik = 80, 443, 8082

## Como usar

Acesse http://client.local/echotest.html, tudo que você escrever deve ser repetido pelo servidor GRPC.

O caminho será:

    - User --> Traefik --> Client GRPC 
    -                  --> Envoy --> GRPC Server

## Docker-Compose.yml

Você deve usar o Swarm para iniciar este arquivo:
docker network create -d overlay proxy_net
docker stack deploy -c docker-compose.yml grpclab