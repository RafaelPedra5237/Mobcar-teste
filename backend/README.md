# MobCar — Back-end

API do MobCar, plataforma de denúncias de infrações de trânsito.

## Stack

- Java 21
- Spring Boot 4.1.0 (Spring MVC, Validation, Actuator)
- Maven

## Pré-requisitos

- JDK 21 (`java -version`)
- Maven 3.9+ (`mvn -v`) — ou gere o wrapper, veja abaixo

## Como executar

```bash
cd backend
mvn clean verify        # compila e roda os testes
mvn spring-boot:run     # sobe a API em http://localhost:8080
```

Teste: abra http://localhost:8080/actuator/health — deve responder `{"status":"UP"}`.

## Maven Wrapper (opcional)

Para quem não tem Maven instalado, gere o wrapper uma vez e versione os arquivos.
O tipo `only-script` não cria `.jar` (o repositório rastreia `*.jar` no Git LFS):

```bash
mvn wrapper:wrapper -Dtype=only-script
./mvnw spring-boot:run
```

## Estrutura

```
backend/
├── pom.xml
└── src/
    ├── main/
    │   ├── java/br/com/mobcar/
    │   │   ├── MobcarApplication.java   # ponto de entrada
    │   │   ├── config/                  # CORS, segurança, beans
    │   │   ├── controller/              # endpoints REST
    │   │   ├── service/                 # regras de negócio
    │   │   ├── repository/              # persistência
    │   │   ├── domain/                  # entidades
    │   │   ├── dto/                     # requests/responses
    │   │   └── exception/               # erros e handler global
    │   └── resources/application.yml
    └── test/java/br/com/mobcar/MobcarApplicationTests.java
```

## Configuração

| Propriedade | Variável de ambiente | Padrão |
|---|---|---|
| `server.port` | `SERVER_PORT` | `8080` |
| `mobcar.cors.allowed-origins` | `MOBCAR_CORS_ALLOWED_ORIGINS` | `localhost:8443`, `localhost:5173` |
