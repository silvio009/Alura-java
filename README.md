# Adopet Console (Java)

Aplicação de linha de comando (CLI) em **Java 17** para consumir a API do projeto Adopet.

O sistema permite:

- listar abrigos cadastrados;
- cadastrar um novo abrigo;
- listar pets de um abrigo;
- importar pets em lote a partir de um arquivo CSV.

> O projeto Java está dentro da pasta `Alura boas práticas- JAVA/`.

## Estrutura do projeto

```text
Alura boas práticas- JAVA/
├── pom.xml
├── pets.csv
├── src/main/java/br/com/alura
│   ├── AdopetConsoleApplication.java
│   ├── Command.java
│   ├── CommandExecutor.java
│   ├── CadastrarAbrigoCommand.java
│   ├── ListarAbrigoCommand.java
│   ├── ListarPetsDoAbrigoCommand.java
│   ├── ImportarPetsDoAbrigoCommand.java
│   ├── client/ClientHttpConfiguration.java
│   ├── domain/Abrigo.java
│   ├── domain/Pet.java
│   └── service/
│       ├── AbrigoService.java
│       └── PetService.java
└── src/test/java/br/com/alura/service/AbrigoServiceTest.java
```

## Arquitetura (resumo)

A aplicação usa um fluxo simples baseado em comando:

1. `AdopetConsoleApplication` exibe o menu e lê a opção do usuário.
2. A opção escolhida aciona um `Command` (`ListarAbrigoCommand`, `CadastrarAbrigoCommand`, etc.).
3. O comando delega para um serviço (`AbrigoService` ou `PetService`).
4. O serviço usa `ClientHttpConfiguration` para chamadas HTTP (`GET` e `POST`) na API.
5. As respostas são convertidas para objetos de domínio (`Abrigo` e `Pet`) e exibidas no console.

## Pré-requisitos

- Java 17+
- Maven 3.8+
- API Adopet executando em `http://localhost:8080`

## Dependências principais

Definidas no `pom.xml`:

- Gson
- Jackson Databind
- JUnit 5
- Mockito

## Como executar

Entre na pasta do projeto Maven:

```bash
cd "Alura boas práticas- JAVA"
```

Compile:

```bash
mvn clean compile
```

Execute a aplicação de console:

```bash
mvn exec:java -Dexec.mainClass=br.com.alura.AdopetConsoleApplication
```

> Se o plugin `exec-maven-plugin` não estiver configurado no seu ambiente, você também pode executar pela IDE (classe `AdopetConsoleApplication`).

## Como rodar os testes

```bash
cd "Alura boas práticas- JAVA"
mvn test
```

Atualmente existe teste para `AbrigoService` com Mockito para simular chamadas HTTP.

## Importação via CSV

O comando de importação pede:

1. id ou nome do abrigo;
2. caminho do arquivo CSV.

Exemplo de arquivo (`pets.csv`):

```csv
cachorro,Rex,Poodle,5,Marrom,10.5
gato,Mia,Siamês,3,Cinza,3.2
```

Formato esperado por linha:

```text
tipo,nome,raca,idade,cor,peso
```

## Observações

- O cliente foi construído para uso local (`localhost:8080`).
- A aplicação trata erros básicos de status HTTP no console.
- Existe um `api.jar` no repositório, que pode ser usado em cenários de estudo/aula conforme o contexto do curso.
