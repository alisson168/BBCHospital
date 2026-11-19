# 🏥 Sistema de Gerenciamento Hospitalar

Projeto acadêmico de Banco de Dados Relacional desenvolvido utilizando **MySQL**, com o objetivo de organizar e gerenciar informações de um hospital.

O banco de dados permite armazenar e relacionar informações de pacientes, médicos, quartos, internações, consultas e prescrições médicas, garantindo a organização dos dados por meio de chaves primárias, chaves estrangeiras e relacionamentos.

## 📌 Contextualização

A administração de um hospital envolve diversas informações que precisam ser armazenadas, organizadas e consultadas constantemente.

O cadastro de pacientes, o controle de médicos, a disponibilidade de quartos, as internações e o histórico de consultas são processos fundamentais para o funcionamento de uma instituição hospitalar.

Quando essas informações não estão organizadas em um sistema adequado, podem ocorrer problemas como:

- Dificuldade para localizar informações dos pacientes.
- Falta de organização dos registros de consultas.
- Dificuldade no acompanhamento das internações.
- Falta de controle sobre os quartos hospitalares.
- Dificuldade para consultar prescrições médicas.
- Repetição e inconsistência de informações.

## 🎯 Proposta

Desenvolver um banco de dados relacional utilizando MySQL para centralizar e organizar as informações hospitalares.

A estrutura foi projetada para conectar diferentes setores do hospital por meio de relacionamentos entre tabelas, facilitando consultas, verificações e o gerenciamento das informações.

O projeto também utiliza consultas SQL para gerar relatórios sobre faturamento, atendimentos médicos, internações, convênios e prescrições.

## ⚙️ Tecnologias utilizadas

- **MySQL 8.0:** Sistema de gerenciamento de banco de dados relacional.
- **MySQL Workbench:** Ferramenta utilizada para executar comandos SQL, administrar o banco e visualizar sua estrutura.
- **SQL:** Linguagem utilizada para criação, manipulação e consulta dos dados.

## 🗄️ Modelagem do Banco de Dados

O banco de dados possui o nome `hospital_db` e é composto por **6 tabelas relacionadas**.

As tabelas são:

1. `pacientes`
2. `medicos`
3. `quartos`
4. `internacoes`
5. `consultas`
6. `prescricoes`

### Diagrama de Entidade-Relacionamento (DER)

O Diagrama de Entidade-Relacionamento apresenta a estrutura do banco de dados, suas entidades, atributos e os relacionamentos entre as tabelas.

**Imagem do DER:**

<!-- Adicione aqui a imagem do Diagrama de Entidade-Relacionamento. -->

## 🚀 Como executar o projeto

### Pré-requisitos

Antes de executar o projeto, é necessário possuir:

- MySQL 8.0 ou superior.
- MySQL Workbench ou outra ferramenta compatível com MySQL.
- O arquivo contendo o script SQL do projeto.

### 1. Abrir o script SQL

Abra o MySQL Workbench e conecte-se ao seu servidor MySQL.

Em seguida:

1. Acesse **File → Open SQL Script**.
2. Selecione o arquivo SQL do projeto.
3. Aguarde o carregamento do script.

### 2. Criar o banco de dados e executar o script

O próprio script possui os comandos responsáveis pela criação do banco de dados:

```sql
CREATE DATABASE IF NOT EXISTS hospital_db;

USE hospital_db;
```

Após abrir o arquivo, execute o script completo pelo botão de raio (⚡).

A execução realiza as seguintes operações:

- Criação do banco de dados `hospital_db`.
- Remoção das tabelas preexistentes.
- Criação das seis tabelas.
- Definição das chaves primárias e estrangeiras.
- Criação dos índices.
- Inserção dos dados fictícios.
- Execução das dez consultas SQL.

**Atenção:** O script contém comandos `DROP TABLE IF EXISTS`. Portanto, executá-lo novamente remove as tabelas existentes e seus registros antes de recriá-las. Não execute o script em um banco com dados importantes que não possam ser apagados.

### 3. Verificar a criação do banco

Após executar o script, utilize:

```sql
USE hospital_db;

SHOW TABLES;
```

O resultado deverá apresentar as seis tabelas:

```text
pacientes
medicos
quartos
internacoes
consultas
prescricoes
```

Para conferir os registros inseridos, execute:

```sql
SELECT * FROM pacientes;
SELECT * FROM medicos;
SELECT * FROM quartos;
SELECT * FROM internacoes;
SELECT * FROM consultas;
SELECT * FROM prescricoes;
```

## 📋 Modelagem Lógica

A seguir estão apresentadas as principais tabelas do banco de dados e seus respectivos atributos.

### 1. Pacientes

Armazena as informações cadastrais dos pacientes atendidos pelo hospital.

| Campo | Tipo | Descrição |
|---|---|---|
| id_paciente | INT | Chave primária e identificação do paciente |
| nome_paciente | VARCHAR(100) | Nome completo do paciente |
| cpf | CHAR(14) | CPF único do paciente |
| data_nascimento | DATE | Data de nascimento |
| telefone_paciente | CHAR(15) | Telefone para contato |
| convenio | CHAR(50) | Convênio médico |

**Na prática:** Essa tabela permite armazenar os dados pessoais dos pacientes e identificar cada um por meio de seu ID e CPF.

<!-- Adicione aqui uma captura de tela da tabela pacientes. -->

### 2. Médicos

Armazena os dados dos profissionais responsáveis pelos atendimentos médicos.

| Campo | Tipo | Descrição |
|---|---|---|
| id_medico | INT | Chave primária e identificação do médico |
| nome_medico | CHAR(100) | Nome do médico |
| crm | CHAR(12) | Registro profissional único |
| especialidade | CHAR(50) | Especialidade médica |

**Na prática:** Permite organizar os profissionais do hospital, identificando suas especialidades e registros no CRM.

<!-- Adicione aqui uma captura de tela da tabela medicos. -->

### 3. Quartos

Responsável pelo armazenamento das informações dos quartos hospitalares.

| Campo | Tipo | Descrição |
|---|---|---|
| id_quarto | INT | Chave primária |
| numero_quarto | CHAR(3) | Número único do quarto |
| andar | CHAR(3) | Andar onde o quarto está localizado |
| tipo_quarto | CHAR(30) | Categoria do quarto |
| status_quarto | CHAR(20) | Situação atual do quarto |

**Na prática:** Permite controlar os quartos disponíveis e ocupados, além de identificar suas categorias, como UTI, Enfermaria, Apartamento e Suíte VIP.

<!-- Adicione aqui uma captura de tela da tabela quartos. -->

### 4. Internações

Registra as internações dos pacientes e os quartos utilizados durante o período de permanência no hospital.

| Campo | Tipo | Descrição |
|---|---|---|
| id_internacao | INT | Chave primária |
| id_paciente | INT | Chave estrangeira de pacientes |
| id_quarto | INT | Chave estrangeira de quartos |
| data_entrada | DATE | Data de entrada do paciente |
| data_saida | DATE | Data de saída do paciente |
| valor_diaria | DECIMAL(10,2) | Valor da diária hospitalar |

**Na prática:** Permite acompanhar o histórico de internações, identificando os pacientes, os quartos utilizados e os valores das diárias.

<!-- Adicione aqui uma captura de tela da tabela internacoes. -->

### 5. Consultas

Armazena os atendimentos realizados pelos médicos aos pacientes.

| Campo | Tipo | Descrição |
|---|---|---|
| id_consulta | INT | Chave primária |
| data_consulta | DATETIME | Data e horário da consulta |
| status_consulta | CHAR(20) | Situação da consulta |
| valor_consulta | DECIMAL(10,2) | Valor do atendimento |
| id_paciente | INT | Chave estrangeira de pacientes |
| id_medico | INT | Chave estrangeira de medicos |

**Na prática:** Permite consultar o histórico de atendimentos, identificar os médicos responsáveis e acompanhar os valores cobrados.

<!-- Adicione aqui uma captura de tela da tabela consultas. -->

### 6. Prescrições

Armazena os medicamentos e as orientações prescritas durante as consultas médicas.

| Campo | Tipo | Descrição |
|---|---|---|
| id_prescricao | INT | Chave primária |
| id_consulta | INT | Chave estrangeira de consultas |
| medicamento | CHAR(100) | Nome do medicamento |
| dosagem | CHAR(50) | Orientação de uso |
| quantidade | CHAR(30) | Quantidade prescrita |

**Na prática:** Permite registrar os medicamentos indicados pelos médicos, suas dosagens e respectivas quantidades.

<!-- Adicione aqui uma captura de tela da tabela prescricoes. -->

## 🔗 Relacionamentos e Cardinalidade

O banco de dados utiliza relacionamentos para conectar informações de diferentes tabelas, evitando a repetição desnecessária de dados.

### Relacionamentos 1:N (Um para Muitos)

- **Pacientes → Internações:** Um paciente pode possuir várias internações, mas cada internação pertence a um único paciente.
- **Quartos → Internações:** Um quarto pode estar associado a várias internações ao longo do tempo, mas cada internação utiliza um único quarto.
- **Pacientes → Consultas:** Um paciente pode realizar várias consultas, mas cada consulta pertence a um único paciente.
- **Médicos → Consultas:** Um médico pode realizar várias consultas, mas cada consulta está vinculada a um único médico.
- **Consultas → Prescrições:** Uma consulta pode possuir várias prescrições, mas cada prescrição pertence a uma única consulta.

### Integridade referencial

Os relacionamentos são implementados por meio de chaves estrangeiras (FK), garantindo que os registros relacionados respeitem as referências existentes no banco de dados.

As chaves primárias (PK) identificam exclusivamente cada registro, enquanto as chaves estrangeiras conectam as tabelas.

## 📊 Índices e Otimização

Foram criados índices para facilitar buscas frequentes e melhorar o desempenho de determinadas consultas.

| Índice | Tabela | Campo |
|---|---|---|
| idx_pacientes_nome | pacientes | nome_paciente |
| idx_medicos_especialidade | medicos | especialidade |
| idx_consultas_data | consultas | data_consulta |

Além desses índices, o banco utiliza índices associados às chaves primárias, às restrições de unicidade e às chaves estrangeiras.

## 📝 Consultas SQL

O projeto possui **10 consultas SQL** desenvolvidas para extrair informações importantes sobre o funcionamento do hospital.

Foram utilizados recursos da linguagem SQL, como:

- **SELECT:** Consultar informações armazenadas.
- **WHERE:** Filtrar registros de acordo com condições.
- **INNER JOIN:** Relacionar informações de diferentes tabelas.
- **GROUP BY:** Agrupar registros.
- **ORDER BY:** Ordenar os resultados.
- **COUNT():** Contabilizar registros.
- **SUM():** Calcular valores acumulados.
- **AVG():** Calcular médias.
- **ROUND():** Arredondar valores numéricos.
- **LIKE:** Pesquisar padrões de texto.
- **IN:** Verificar se um valor pertence a uma lista.

### 1. Faturamento Total de Consultas por Convênio

**Contextualização e Situação-Problema:** O setor financeiro necessita identificar o faturamento total das consultas realizadas por pacientes vinculados a convênios que possuem a palavra "Saúde" em seu nome.

A consulta agrupa os resultados por convênio e apresenta o faturamento em ordem decrescente.

**Recursos utilizados:** INNER JOIN, WHERE, LIKE, SUM(), GROUP BY e ORDER BY.

<!-- Adicione aqui uma captura de tela do resultado da consulta 1. -->

### 2. Média do Valor de Consulta por Especialidade Médica

**Contextualização e Situação-Problema:** A administração hospitalar deseja verificar o valor médio das consultas realizadas por médicos de especialidades relacionadas à Cardiologia.

A consulta identifica especialidades que contêm a palavra "Cardio" e calcula a média dos valores das consultas.

**Recursos utilizados:** INNER JOIN, WHERE, LIKE, AVG(), ROUND() e GROUP BY.

<!-- Adicione aqui uma captura de tela do resultado da consulta 2. -->

### 3. Valor Médio das Diárias por Tipo de Quarto

**Contextualização e Situação-Problema:** A gestão hospitalar necessita analisar o valor médio das diárias cobradas nas internações realizadas em quartos dos tipos "Apartamento" e "UTI".

A consulta agrupa os resultados por tipo de quarto.

**Recursos utilizados:** INNER JOIN, WHERE, IN, AVG(), ROUND() e GROUP BY.

<!-- Adicione aqui uma captura de tela do resultado da consulta 3. -->

### 4. Total de Consultas Realizadas por Médico

**Contextualização e Situação-Problema:** A diretoria do hospital deseja identificar a quantidade de consultas realizadas por cada médico e o valor total arrecadado com esses atendimentos.

São consideradas apenas consultas com status "Realizada" ou "Finalizada".

**Recursos utilizados:** INNER JOIN, WHERE, IN, COUNT(), SUM(), GROUP BY e ORDER BY.

<!-- Adicione aqui uma captura de tela do resultado da consulta 4. -->

### 5. Soma de Diárias por Paciente com Sobrenome "Silva"

**Contextualização e Situação-Problema:** O setor financeiro precisa identificar os pacientes que possuem o sobrenome "Silva" e calcular a soma dos valores de suas diárias de internação registradas.

A consulta agrupa os resultados por paciente e organiza os valores em ordem decrescente.

**Recursos utilizados:** INNER JOIN, WHERE, LIKE, SUM(), GROUP BY e ORDER BY.

<!-- Adicione aqui uma captura de tela do resultado da consulta 5. -->

### 6. Contagem de Prescrições por Status da Consulta

**Contextualização e Situação-Problema:** A farmácia hospitalar deseja identificar a quantidade de prescrições de medicamentos que contenham "Dipirona" ou "Paracetamol", agrupando os resultados pelo status da consulta correspondente.

**Recursos utilizados:** INNER JOIN, WHERE, LIKE, OR, COUNT() e GROUP BY.

<!-- Adicione aqui uma captura de tela do resultado da consulta 6. -->

### 7. Média de Valor de Consultas por Convênio e Especialidade

**Contextualização e Situação-Problema:** O setor administrativo deseja analisar o valor médio das consultas realizadas por pacientes vinculados a convênios que contenham "Unimed", considerando também a especialidade dos médicos responsáveis.

A consulta apresenta a quantidade de consultas e a média dos valores para cada combinação de convênio e especialidade.

**Recursos utilizados:** INNER JOIN, WHERE, LIKE, COUNT(), AVG(), ROUND(), GROUP BY e ORDER BY.

<!-- Adicione aqui uma captura de tela do resultado da consulta 7. -->

### 8. Média de Diária de Internação por Convênio em Quartos de UTI

**Contextualização e Situação-Problema:** A administração hospitalar deseja analisar o valor médio das diárias de internação por convênio, considerando exclusivamente os quartos classificados como "UTI".

A consulta também apresenta a quantidade de internações registradas por convênio.

**Recursos utilizados:** INNER JOIN, WHERE, COUNT(), AVG(), ROUND(), GROUP BY e ORDER BY.

<!-- Adicione aqui uma captura de tela do resultado da consulta 8. -->

### 9. Medicamentos Prescritos por Médico em Consultas Realizadas

**Contextualização e Situação-Problema:** A comissão de farmácia e terapêutica deseja identificar a quantidade de itens prescritos por cada médico nas consultas que possuem o status "Realizada".

A consulta relaciona prescrições, consultas e médicos para apresentar o total de itens prescritos por profissional.

**Recursos utilizados:** INNER JOIN, WHERE, COUNT() e GROUP BY.

<!-- Adicione aqui uma captura de tela do resultado da consulta 9. -->

### 10. Valor Total e Média de Consultas por Paciente

**Contextualização e Situação-Problema:** O setor financeiro deseja gerar um relatório contendo a quantidade de consultas, o valor total e o valor médio dos atendimentos realizados por pacientes cujos nomes começam com a letra "M".

**Recursos utilizados:** INNER JOIN, WHERE, LIKE, COUNT(), SUM(), AVG(), ROUND(), GROUP BY e ORDER BY.

<!-- Adicione aqui uma captura de tela do resultado da consulta 10. -->

Essas consultas permitem gerar relatórios e analisar informações relacionadas aos pacientes, profissionais, atendimentos, convênios, internações e prescrições médicas.

Projeto desenvolvido como atividade acadêmica de Banco de Dados

## 📚 Objetivo Educacional

Este projeto tem como finalidade colocar em prática os conceitos de Banco de Dados Relacionais, incluindo:

- Criação e estruturação de bancos de dados.
- Desenvolvimento de tabelas e seus respectivos atributos.
- Definição de chaves primárias e estrangeiras.
- Compreensão de relacionamentos e cardinalidade.
- Inserção e manipulação de registros.
- Aplicação de integridade referencial.
- Criação de índices para otimização de buscas.
- Desenvolvimento de consultas SQL utilizando JOIN, GROUP BY e funções de agregação.

**Observação:** Projeto desenvolvido para fins educacionais. Os dados utilizados são fictícios e destinados exclusivamente a testes, estudos e demonstrações.
