# 💈 Sistema de Agendamento para Barbearia

Sistema desktop para agendamento de serviços de uma barbearia, desenvolvido em **Java** com interface gráfica **Swing** e banco de dados **MySQL**.

## ✨ Funcionalidades

- Cadastrar clientes, com máscara e validação de telefone e CPF
- Listar clientes, com caixa de pesquisa
- Excluir clientes por uma lista clicável
- Agendar serviços (corte de cabelo, barba ou combo), escolhendo data e hora separadamente
- Bloquear horários no passado
- Garantir intervalo mínimo de 30 minutos entre agendamentos
- Listar agendamentos, com data e hora separadas
- Cancelar agendamentos por uma lista clicável
- Registrar todas as operações no arquivo `sistema_log.txt`

### Serviços e preços

| Serviço                 | Preço  |
|-------------------------|--------|
| Corte de cabelo         | R$ 30  |
| Barba                   | R$ 25  |
| Combo (Corte + Barba)   | R$ 55  |

## 🧰 Tecnologias

- Java (JDK 17 ou superior)
- Swing (interface gráfica)
- MySQL 8
- JDBC (MySQL Connector/J 9.3.0)

## 📁 Estrutura do projeto

O código está no arquivo `AppBarbeariaV3.zip`. Depois de extrair, a estrutura é:

```
AppBarbeariaV3/
├── lib/
│   └── mysql-connector-j-9.3.0.jar
├── src/
│   ├── Main.java           # ponto de entrada
│   ├── SistemaGUI.java     # janela principal
│   ├── SalaoDAO.java       # regras de negócio e acesso ao banco
│   ├── Database.java       # conexão com o MySQL
│   └── Logger.java         # geração do log
├── salaodb.sql             # script do banco de dados
└── README.md
```

## 🗄️ Banco de dados

Banco: `salaodb`

```sql
CREATE TABLE clientes (
  id INT AUTO_INCREMENT PRIMARY KEY,
  nome VARCHAR(100) NOT NULL,
  cpf VARCHAR(14),
  telefone VARCHAR(20)
);

CREATE TABLE agendamentos (
  id INT AUTO_INCREMENT PRIMARY KEY,
  cliente_id INT,
  data_hora DATETIME,
  servico VARCHAR(100),
  preco DECIMAL(10,2),
  FOREIGN KEY (cliente_id) REFERENCES clientes(id)
);
```

## 🚀 Como executar

### 1. Pré-requisitos

- JDK 17 ou superior instalado e configurado no PATH
- MySQL em execução local (porta padrão `3306`)

### 2. Preparar o banco

Crie o banco e importe o script `salaodb.sql`:

```sql
CREATE DATABASE salaodb;
```

```bash
mysql -u root -p salaodb < salaodb.sql
```

Alternativa: no MySQL Workbench, vá em **Server → Data Import** e selecione o arquivo `salaodb.sql`.

### 3. Configurar as credenciais

Abra `src/Database.java` e ajuste o usuário e a senha para os do seu MySQL:

```java
String user = "root";
String password = "admin";
```

### 4. Compilar

```bash
cd AppBarbeariaV3
javac -encoding UTF-8 -cp "lib/mysql-connector-j-9.3.0.jar" -d bin src/*.java
```

### 5. Executar

**Windows:**
```bash
java -cp "bin;lib/mysql-connector-j-9.3.0.jar" Main
```

**Linux / macOS:**
```bash
java -cp "bin:lib/mysql-connector-j-9.3.0.jar" Main
```

### Pela IDE (Eclipse, IntelliJ, VS Code)

1. Abra a pasta do projeto.
2. Adicione `lib/mysql-connector-j-9.3.0.jar` como biblioteca externa.
3. Marque `src/` como pasta de código-fonte.
4. Execute a classe **`Main`**.

## 📝 Logs

Todas as ações relevantes (cadastro, exclusão, agendamento, cancelamento e erros) são registradas, com data e hora, em `sistema_log.txt`.

## 🔮 Ideias para evolução

- Relatórios de faturamento
- Mais serviços e profissionais
- Migração da interface para JavaFX
- Integração com Hibernate/JPA
