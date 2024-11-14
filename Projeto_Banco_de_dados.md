# Projeto conceitual de banco de dados
## Objetivo
  O objetivo deste projeto é identificar as etapas de um projeto de banco de dados, reconhecer elementos do diagrama de entidade Relacionamento, compreender a modelagem de entidades e relacionamentos e a modelagem de atributos.
## Introdução 
  Implementar um banco de dados é uma automatização do negócio ou parte dele. O banco de dados representa algum aspecto do mundo real e para aplicar ao negócio é necessário conhece-lo.
  A construção de um banco de dados acontece em etapas bem definidas( levantamento de requisitos, projeto conceitual, projeto logico e projeto fisico.
  Ao longo delas perceberemos que não entraremos muito detalhadamente em como os dados são organizados fisicamente, mas nesse momento de projeto conceitual o mais importante são os usuários enxergarem
  como o banco de dados esta estruturado para o negócio. Para isso faremos o diagrama de relacionamento(DER).
## Levantamento de requisitos
  Essa é uma das fases cruciais no desenvolvimento do sistema. O objetivo de todo sistema é resolver algum problema,
  mas como fazer isso? Na entrevista de requisitos é onde descobrimos quais as necessidades que o cliente tem em cima
  desse problema que ele deseja resolver. Fazer essa etapa muito bem feita é essencial para a construção de um esquema
  eficiente. Por exemplo uma oficina o cliente tem um carro(relacionamento) o carro tem placar, modelo, ano, dono(atributos)
  então no meu banco de dados precisam transformar esses dados de forma organizada e clara para que o usuário(mecanico,
  dono do carro) consiga localizar o carro, quem é o dono e quais serviços foram feitos. Nesse sentido precisamos ter
  conhecimento sobre o negócio porque existem informações que não não necessárias e serão excluídas do nosso minimundo,
  representado no nosso banco de dados, imagine qual seria o objetivo de colocar como atributo a cor da roupa do cliente?
  Essa informação seria completamente irrelevante para nosso banco de dados.
  ### Levantamento de requisitos do nosso projeto
  Imaginemos que fomos convidados a participar de um projeto para controlar as incrições de alunos em uma escola de treinamento
  na área de tenologia da informação. Ao realizar as entrevistas levantamos os seguintes requisitos:
  - A escola planeja diversos cursos. Cada um possui nome, descrição, carga horaria, e é identificado por um codigo unico;
  - A escola armazena o nome, a data de nascimento, o cpf, o email e um telefone de cada cliente tambem identificado por codigo unico;
  - Quando um cliente faz a inscrição em determinado curso, é necessario armazenas a data. Caso seja cancelado é preciso saber quando ocorreu esse evento. Um cliente pode fazer diversos cursos.
## Projeto conceitual
  O projeto conceitual de banco de dados define a estrutura de dados de forma independente do sistema de gerenciamento de banco de dados (SGBD) e das especificações físicas. Focado em representar
  informações essenciais e suas relações, esse modelo usa diagramas entidade-relacionamento (ER) para identificar entidades, atributos e relacionamentos. Ele serve como uma base inicial para a 
  criação de um banco de dados, garantindo organização e consistência lógica antes de se avançar para o projeto lógico e físico.
  ### No nosso projeto

![diagrama DER.JPG](https://github.com/Leorehin/estudosSQL/blob/main/diagrama%20DER.JPG)
  Diagrama ER

![Diagrama UML](https://github.com/Leorehin/estudosSQL/blob/main/diagrama%20UML.JPG)
Diagrama UML

## Modelo logico
O modelo lógico de banco de dados transforma o projeto conceitual em um formato compatível com o SGBD escolhido. Ele define tabelas, colunas, tipos de dados, chaves primárias e estrangeiras, visando a estruturação eficiente dos dados e a integridade referencial. É a etapa intermediária entre o modelo conceitual e o modelo físico, alinhando o design do banco com os requisitos específicos do sistema.

### No nosso projeto
  ```
  erDiagram
    CLIENTE {
        int id_cliente PK
        string nome
        date data_nascimento
        string cpf
        string email
        string telefone
    }

    CURSO {
        int id_curso PK
        string nome
        string descricao
        int carga_horaria
    }

    INSCRICAO {
        int id_inscricao PK
        int id_cliente FK
        int id_curso FK
        date data_inscricao
        date data_cancelamento
    }

    CLIENTE ||--o{ INSCRICAO : "faz"
    CURSO ||--o{ INSCRICAO : "tem"

```
Diagrama de classes
