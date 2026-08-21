# Calculadora SOAP (Java)

Serviço web SOAP simples realizado na matéria de Programação Web II, escrito em Java com JAX-WS, que expõe operações
básicas de uma calculadora (soma, subtração, multiplicação e divisão).
O projeto contém um servidor que publica o serviço e um cliente de exemplo
que consome esse serviço.

## Tecnologias

- Java 8
- Maven
- JAX-WS (`javax.jws`, `javax.xml.ws`, `com.sun.xml.ws:jaxws-rt`)

## Estrutura do projeto

```
calculadora-soap-main/
├── pom.xml
└── src/main/java/calc/
    ├── CalculadoraServer.java          # Interface do serviço (contrato SOAP)
    ├── CalculadoraServerImpl.java      # Implementação das operações
    ├── CalculadoraServerPublisher.java # Publica o serviço em um endpoint HTTP
    └── CalculadoraClient.java          # Cliente de exemplo que consome o serviço
```

## Serviço

A interface `CalculadoraServer` define o contrato do web service, usando
binding SOAP no estilo RPC, com os seguintes métodos:

| Método          | Parâmetros            | Retorno | Descrição              |
|-----------------|------------------------|---------|-------------------------|
| `soma`          | `float num1, float num2` | `float` | Soma dois números       |
| `subtracao`     | `float num1, float num2` | `float` | Subtrai dois números    |
| `multiplicacao` | `float num1, float num2` | `float` | Multiplica dois números |
| `divisao`       | `float num1, float num2` | `float` | Divide dois números     |

A implementação está em `CalculadoraServerImpl`.

## Como executar

### Pré-requisitos

- JDK 8 ou superior
- Maven instalado

### 1. Compilar o projeto

```bash
mvn clean compile
```

### 2. Iniciar o servidor

Execute a classe `CalculadoraServerPublisher`, que publica o serviço no
endereço `http://127.0.0.1:9876/calc`:

```bash
mvn exec:java -Dexec.mainClass="calc.CalculadoraServerPublisher"
```

Com o servidor rodando, o WSDL fica disponível em:

```
http://127.0.0.1:9876/calc?wsdl
```

### 3. Executar o cliente de exemplo

Em outro terminal, com o servidor já em execução, rode o cliente:

```bash
mvn exec:java -Dexec.mainClass="calc.CalculadoraClient"
```

Saída esperada:

```
Soma (5+1): 6.0
Subtracao (5-1): 4.0
Multiplicacao (5*1): 5.0
Divisao (5/1): 5.0
```

> Observação: caso o plugin `exec-maven-plugin` não esteja configurado no
> `pom.xml`, é possível executar as classes diretamente pela sua IDE
> (IntelliJ IDEA, Eclipse, etc.) ou via `java -cp` apontando para as
> dependências baixadas pelo Maven.
