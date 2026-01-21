# Build-Run-TesteUnitario

[![Java](https://img.shields.io/badge/Java-21-orange.svg)](https://www.oracle.com/java/)
[![Maven](https://img.shields.io/badge/Maven-3.x-blue.svg)](https://maven.apache.org/)
[![JUnit 5](https://img.shields.io/badge/JUnit-5.11.4-green.svg)](https://junit.org/junit5/)
[![Mockito](https://img.shields.io/badge/Mockito-5.15.2-red.svg)](https://site.mockito.org/)

## 📋 Sobre o Projeto

Este projeto demonstra boas práticas de testes unitários em Java utilizando JUnit 5 e Mockito. É um projeto educacional que apresenta diferentes técnicas e padrões de testes, incluindo testes parametrizados, uso de mocks, e organização de testes.

## 🛠️ Tecnologias Utilizadas

### Core
- **Java**: 21
- **Maven**: Gerenciador de dependências e build
- **Encoding**: UTF-8

### Dependências de Teste

| Dependência | Versão | Descrição |
|-------------|--------|-----------|
| JUnit Jupiter API | 5.11.4 | Framework de testes unitários |
| JUnit Jupiter Params | 5.11.4 | Suporte para testes parametrizados |
| Mockito Core | 5.15.2 | Framework para criação de mocks |
| Mockito JUnit Jupiter | 5.15.2 | Integração Mockito com JUnit 5 |

## 📁 Estrutura do Projeto

```
src/
├── main/java/tech/buildrun/
│   ├── Calculadora.java                      # Classe com operações matemáticas
│   ├── authms/                               # Módulo de autenticação
│   │   ├── AuthService.java                  # Serviço de autenticação
│   │   ├── User.java                         # Modelo de usuário
│   │   ├── UserRepository.java               # Interface do repositório
│   │   └── InMemoryUserRepository.java       # Implementação em memória
│   ├── ecommerce/                            # Módulo de e-commerce
│   │   ├── Order.java                        # Modelo de pedido
│   │   ├── OrderService.java                 # Serviço de pedidos
│   │   ├── OrderRepository.java              # Interface do repositório
│   │   └── RealOrderRepository.java          # Implementação real
│   └── mockito/                              # Exemplos com Mockito
│       ├── UserService.java                  # Serviço de usuário
│       ├── Database.java                     # Interface de database
│       └── RealDatabase.java                 # Implementação real
│
└── test/java/tech/buildrun/
    ├── CalculadoraTest.java                  # Testes da calculadora
    ├── authms/
    │   ├── AuthServiceTest.java              # Testes do serviço de auth
    │   └── UserTest.java                     # Testes do modelo User
    ├── ecommerce/
    │   ├── OrderServiceTest.java             # Testes do serviço de pedidos
    │   └── RealOrderRepositoryTest.java      # Testes do repositório
    └── mockito/
        └── UserServiceTest.java              # Testes com Mockito
```

## 🚀 Como Executar

### Pré-requisitos

- Java 21 ou superior instalado
- Maven 3.x instalado
- Variável de ambiente `JAVA_HOME` configurada

### Compilar o Projeto

```bash
mvn clean compile
```

### Executar os Testes

Para executar todos os testes:

```bash
mvn test
```

Para executar testes de uma classe específica:

```bash
mvn test -Dtest=CalculadoraTest
```

### Gerar Relatório de Testes

```bash
mvn surefire-report:report
```

O relatório será gerado em `target/site/surefire-report.html`

### Empacotar o Projeto

```bash
mvn package
```

## 📚 Exemplos de Testes

### Testes Básicos com JUnit 5

O projeto demonstra testes básicos com a classe `Calculadora`:

```java
@Test
@DisplayName("Should add two numbers")
public void shouldAddTwoNumbers() {
    // Arrange
    int a = 2;
    int b = 3;

    // Act
    var output = calculadora.somar(a, b);

    // Assert
    assertEquals(5, output);
}
```

### Testes com Nested Classes

Organização de testes relacionados usando `@Nested`:

```java
@Nested
class somar {
    @Test
    void shouldAddTwoNumbers() { ... }
    
    @Test
    void shouldAddWhenTwoNumbersIsZero() { ... }
}
```

### Testes de Exceções

Validação de exceções esperadas:

```java
@Test
@DisplayName("Should throw exception when divide to zero")
void shouldThrowExceptionWhenDivideToZero() {
    var ex = assertThrows(ArithmeticException.class, () -> {
        calculadora.dividir(4, 0);
    });
    
    assertEquals("Divisão por zero não permitida.", ex.getMessage());
}
```

### Testes com Mockito

Criação de mocks para isolar dependências:

```java
@Mock
private Database database;

@InjectMocks
private UserService userService;

@Test
void testWithMock() {
    when(database.findUser(anyString())).thenReturn(new User("test"));
    // ...
}
```

## 🎯 Funcionalidades Testadas

### Calculadora
- ✅ Operações básicas: soma, subtração, multiplicação, divisão
- ✅ Operações avançadas: potência, raiz quadrada
- ✅ Funções auxiliares: valor absoluto, verificação de paridade
- ✅ Funções matemáticas: verificação de números primos, máximo, mínimo
- ✅ Tratamento de exceções

### Módulo de Autenticação (authms)
- ✅ Testes de serviço de autenticação
- ✅ Testes de modelo de usuário
- ✅ Testes de repositório

### Módulo de E-commerce
- ✅ Testes de serviço de pedidos
- ✅ Testes de repositório de pedidos

### Exemplos com Mockito
- ✅ Criação e uso de mocks
- ✅ Injeção de dependências mockadas
- ✅ Verificação de comportamento

## 📖 Padrões e Boas Práticas

Este projeto demonstra:

1. **Padrão AAA (Arrange-Act-Assert)**: Organização clara dos testes
2. **Testes Isolados**: Cada teste é independente e não depende de outros
3. **Nomes Descritivos**: Uso de `@DisplayName` para descrições claras
4. **Nested Tests**: Agrupamento lógico de testes relacionados
5. **Mock Objects**: Isolamento de dependências usando Mockito
6. **Testes de Exceções**: Verificação de comportamentos de erro
7. **Testes Parametrizados**: Reutilização de lógica de teste com diferentes entradas

## 📝 Informações do Projeto

- **Group ID**: tech.buildrun
- **Artifact ID**: unittest
- **Version**: 1.0-SNAPSHOT
- **Packaging**: JAR (default)

## 🤝 Contribuindo

Este é um projeto educacional. Sinta-se à vontade para:

1. Fork o projeto
2. Criar uma branch para sua feature (`git checkout -b feature/NovaFeature`)
3. Commit suas mudanças (`git commit -m 'Adiciona nova feature'`)
4. Push para a branch (`git push origin feature/NovaFeature`)
5. Abrir um Pull Request

## 📄 Licença

Este projeto é distribuído sob a licença apropriada. Consulte o arquivo LICENSE para mais detalhes.

## 👤 Autor

**Build Run Tech**

- Group: tech.buildrun

## 🔗 Links Úteis

- [JUnit 5 Documentation](https://junit.org/junit5/docs/current/user-guide/)
- [Mockito Documentation](https://javadoc.io/doc/org.mockito/mockito-core/latest/org/mockito/Mockito.html)
- [Maven Documentation](https://maven.apache.org/guides/)
- [Java 21 Documentation](https://docs.oracle.com/en/java/javase/21/)