Rastreador de Encomendas
Este é um projeto simples de rastreamento de encomendas implementado em Java. O projeto utiliza MySQL como banco de dados para armazenar informações sobre usuários, encomendas e status.

Estrutura do Projeto
less
Copy code
├── src/
│   ├── main/
│   │   ├── java/
│   │   │   ├── entities/                           // Pacote para as entidades
│   │   │   │   ├── Usuario.java                    // Classe para a entidade Usuário
│   │   │   │   ├── Encomenda.java                  // Classe para a entidade Encomenda
│   │   │   │   └── Status.java                     // Classe para a entidade Status
│   │   │   ├── interfaces/                         // Pacote para as interfaces dos serviços
│   │   │   │   ├── UsuarioService.java             // Interface para serviços de Usuário
│   │   │   │   ├── EncomendaService.java           // Interface para serviços de Encomenda
│   │   │   │   └── StatusService.java              // Interface para serviços de Status
│   │   │   ├── services/                           // Pacote para as implementações dos serviços
│   │   │   │   ├── UsuarioServiceImpl.java         // Implementação do serviço de Usuário
│   │   │   │   ├── EncomendaServiceImpl.java       // Implementação do serviço de Encomenda
│   │   │   │   └── StatusServiceImpl.java          // Implementação do serviço de Status
│   │   │   ├── database/                           // Pacote para a conexão com o banco de dados
│   │   │   │   └── DatabaseConnection.java         // Classe para gerenciar a conexão com o MySQL
│   │   │   └── Main.java                           // Classe principal
│   │   └── resources/                              // Recursos adicionais (opcional)
│   └── test/                                       // Pacote para testes (opcional)
├── pom.xml (ou build.gradle)                       // Configuração do projeto
└── README.md                                       // Documentação do projeto
Pré-requisitos
Java 8 ou superior
Maven 3.x
MySQL Server
Configuração
1. Clone o repositório ou baixe os arquivos do projeto.
2. Configure o banco de dados:
Crie um banco de dados no MySQL chamado nome_do_banco (substitua pelo nome desejado).

Execute os seguintes comandos SQL para criar as tabelas necessárias:

sql
Copy code
CREATE TABLE Usuario (
    id_usuario INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(100),
    email VARCHAR(100),
    telefone VARCHAR(15)
);

CREATE TABLE Encomenda (
    id_encomenda INT AUTO_INCREMENT PRIMARY KEY,
    codigo_rastreio VARCHAR(50),
    data_envio DATE,
    id_usuario INT,
    FOREIGN KEY (id_usuario) REFERENCES Usuario(id_usuario)
);

CREATE TABLE Status (
    id_status INT AUTO_INCREMENT PRIMARY KEY,
    id_encomenda INT,
    status VARCHAR(100),
    data_status DATE,
    FOREIGN KEY (id_encomenda) REFERENCES Encomenda(id_encomenda)
);
3. Configurar as credenciais do banco de dados:
Abra o arquivo DatabaseConnection.java e altere as variáveis URL, USER e PASSWORD com as informações de acesso ao seu banco de dados MySQL.

java
Copy code
private static final String URL = "jdbc:mysql://localhost:3306/nome_do_banco"; // Substitua com seu nome de banco
private static final String USER = "usuario"; // Substitua com seu nome de usuário
private static final String PASSWORD = "senha"; // Substitua com sua senha
Executando o Projeto
Navegue até o diretório do projeto.
Compile e instale o projeto com Maven:
bash
Copy code
mvn clean install
Execute o projeto com o comando abaixo, substituindo "main.Main" pela classe principal do seu projeto:
bash
Copy code
mvn exec:java -Dexec.mainClass="main.Main"
Testes
Para executar testes automatizados, você pode usar o Maven com o comando abaixo:

bash
Copy code
mvn test
Contribuições
Sinta-se à vontade para enviar pull requests ou relatar problemas. Para contribuir, siga estas etapas:

Faça um fork deste repositório.
Crie uma nova branch para suas alterações.
Envie um pull request com uma descrição detalhada das mudanças realizadas.