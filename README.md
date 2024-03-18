# SHOES CLICK - STACK

Projetos conceito para utilização de Serviço Rest com Spring Boot

## Projetos:

* **bff-site-shoes**
* **api--customer**
* **api--prodcut**
* **api--product**
* **service--notification**
* **service--payment**
* **eureka-server**
* **server--config-service**
* **server--discovery-stack**
* **config--shoesclick-server (Repositorio das configurações lido pelo server--config-service)**
## Iniciando o Projeto

Os projetos contém alguns exemplos de serviço REST. Os projetos já estão configurados em modo standalone

### Pré requisitos

```
Java 17 : ([https://www.oracle.com/br/java/technologies/javase/jdk17-archive-downloads.html]);

Spring Boot na versão 3.1.9:  (https://mvnrepository.com/artifact/org.springframework.boot/spring-boot-dependencies/3.1.9);

Maven 3.9.5: (https://dlcdn.apache.org/maven/maven-3/3.9.5/binaries/apache-maven-3.9.5-bin.tar.gz)

Eclipse ou Intellij

Docker: Para Rodar o arquivo docker-compose (Contido no projeto principal) que contém a imagem do mysql e do rabbitmq para facilitar a integração

Postman para Testes : (https://www.postman.com/downloads/)
```

## Arquivo openapi para gerar o mock server dos serviços de pagamento:
   IMPORTANTE: Ao gerar o mock, defina as urls dos serviços no 
   arquivo application.yaml do projeto service--payment

```
apidocs-mock.yaml
```

## Rodando local


**Na pasta raiz do projeto, Rode o docker compose Com o comando abaixo:**

```
docker-compose up
```

**Com o postman, ou outra ferramenta, crie um Mock Server a partir da apidocs.yaml que está na raiz:**

```
apidocs-mock.yaml
```



**No Projeto service--payments na pasta src/main/reources/application.yaml, altere as urls base dos mocks conforme exemplo abaixo:**

```
  gateway:
    bankSlipUrl: https://a0bb02cd-0bbc-46d6-915b-36835334ba89.mock.pstmn.io
    pixUrl: https://a0bb02cd-0bbc-46d6-915b-36835334ba89.mock.pstmn.io
    cardUrl: https://a0bb02cd-0bbc-46d6-915b-36835334ba89.mock.pstmn.io
```

**Entre na pasta de cada projeto e rode o comando do maven:**

```
mvn clean install
```

**Em uma IDE, inicie a classe Applicaton.java de cada projeto**


## Rodando com postman

Importe o arquivo abaixo e execute os testes:

```
 Shoes.click - STACK.postman_collection.json
```

## Observação: 

Basicamente alguns serviços carregam informações no banco como produtos, template de email.
Para Conseguir Rodar a integração basta chamar dois serviços do BFF (Pasta BFF do Postman):

* **POST: /customer/save**
* **POST: /order/save**

Pare saber se a integração funcionou corretamente basta olhar as tabelas de logs dos bancos:

* **dbnotification**
* **dbpayment**  

Os projetos estão rodando na porta 5000, pois a intenção e criar uma esteira para efetuar o deploy no kubernetes. 
Então pra rodar local, precisa alterar a porta de todos (do actuator também)

## Autores

* **Clayton Morais de Oliveira**
