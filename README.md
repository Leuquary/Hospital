# Hospital Fundamental
Um pequeno hospital local busca desenvolver um novo sistema que atenda melhor às suas necessidades. Atualmente, parte da operação ainda se apoia em planilhas e arquivos antigos, mas espera-se que esses dados sejam transferidos para o novo sistema assim que ele estiver funcional. Neste momento, é necessário analisar com cuidado as necessidades desse cliente e sugerir uma estrutura de banco de dados adequada por meio de um Diagrama Entidade-Relacionamento.

## Estudo de caso

O hospital necessita de um sistema para sua área clínica que ajude a controlar consultas realizadas. Os médicos podem ser generalistas, especialistas ou residentes e têm seus dados pessoais cadastrados em planilhas digitais. Cada médico pode ter uma ou mais especialidades, que podem ser pediatria, clínica geral, gastroenterologia e dermatologia. Alguns registros antigos ainda estão em formulário de papel, mas será necessário incluir esses dados no novo sistema.

Os pacientes também precisam de cadastro, contendo dados pessoais (nome, data de nascimento, endereço, telefone e e-mail), documentos (CPF e RG) e convênio. Para cada convênio, são registrados nome, CNPJ e tempo de carência.

As consultas também têm sido registradas em planilhas, com data e hora de realização, médico responsável, paciente, valor da consulta ou nome do convênio, com o número da carteira. Também é necessário indicar na consulta qual a especialidade buscada pelo paciente.

Deseja-se ainda informatizar a receita do médico, de maneira que, no encerramento da consulta, ele possa registrar os medicamentos receitados, a quantidade e as instruções de uso. A partir disso, espera-se que o sistema imprima um relatório da receita ao paciente ou permita sua visualização via internet.

## Requisitos do Hospital

**RF001** O sistema deve permitir o cadastro dos profissionais do Hospital, contendo os dados pessoais como nome, CPF, data de nascimento, endereço, telefone e e-mail; seu cargo e suas especialidades.

**RF002** O atendente deve ser capaz de agendar uma consulta para o paciente com os dados: data e hora da realização, 
profissional responsável, paciente, valor da consulta ou convênio e especialidade buscada pelo paciente.

**RF003** O atendente deve ser capaz de cadastrar o paciente, com os dados pessoais como nome, data de nascimento, endereço, telefone, e-mail; documentos (CPF e RG) e os dados do convênio, como número da carteira.

**RF004** O sistema deve registrar o convênio de cada paciente com os dados: nome, número de carteira, CNPJ e tempo de carência.

**RF005** O paciente deve ser capaz de consultar os dados da sua consulta usando seu CPF, por meio do portal online da clínica.

**RF006** O médico deve ser capaz de encerrar a consulta registrando os medicamentos receitados, a quantidade e as instruções de uso.

**RF007** O sistema deve permitir a impressão de relatórios com os dados das consultas dos pacientes.

## Diagrama ER
![alt text](image.png)

# Os Segredos do Hospital
Após a primeira versão do projeto de banco de dados para o sistema hospitalar, notou-se a necessidade de expansão das funcionalidades, incluindo alguns requisitos essenciais a essa versão do software. As funcionalidades em questão são para o controle na internação de pacientes. Será necessário expandir o Modelo ER desenvolvido e montar o banco de dados, criando as tabelas para o início dos testes.

## Estudo de caso
Considere a seguinte descrição e o diagrama ER abaixo:

No hospital, as internações têm sido registradas por meio de formulários eletrônicos que gravam os dados em arquivos. 

Para cada internação, são anotadas a data de entrada, a data prevista de alta e a data efetiva de alta, além da descrição textual dos procedimentos a serem realizados. 

As internações precisam ser vinculadas a quartos, com a numeração e o tipo. 

Cada tipo de quarto tem sua descrição e o seu valor diário (a princípio, o hospital trabalha com apartamentos, quartos duplos e enfermaria).

Também é necessário controlar quais profissionais de enfermaria estarão responsáveis por acompanhar o paciente durante sua internação. Para cada enfermeiro(a), é necessário nome, CPF e registro no conselho de enfermagem (CRE).

A internação, obviamente, é vinculada a um paciente – que pode se internar mais de uma vez no hospital – e a um único médico responsável.

## Requisitos do Hospital

**RF001** O sistema deve permitir o cadastro dos profissionais do Hospital, contendo os dados pessoais como nome, CPF, data de nascimento, endereço, telefone e e-mail; seu cargo e suas especialidades.

**RF002** O atendente deve ser capaz de agendar uma consulta para o paciente com os dados: data e hora da realização, 
profissional responsável, paciente, valor da consulta ou convênio e especialidade buscada pelo paciente.

**RF003** O atendente deve ser capaz de cadastrar o paciente, com os dados pessoais como nome, data de nascimento, endereço, telefone, e-mail; documentos (CPF e RG) e os dados do convênio, como número da carteira.

**RF004** O sistema deve registrar o convênio de cada paciente com os dados: nome, número de carteira, CNPJ e tempo de carência.

**RF005** O paciente deve ser capaz de consultar os dados da sua consulta usando seu CPF, por meio do portal online da clínica.

**RF006** O médico deve ser capaz de encerrar a consulta registrando os medicamentos receitados, a quantidade e as instruções de uso.

**RF007** O sistema deve permitir a impressão de relatórios com os dados das consultas dos pacientes.

**RF008** O sistema deve permitir o registro das internações do paciente, com os dados: data de entrada no hospital, data prevista de alta, data da alta, descrição dos procedimentos, dados do quarto, enfermeiro, médico e paciente.

**RF009** O sistema deve permitir o cadastro dos quartos existentes no hospital, com a numeração, a descrição do quarto, valor diário e tipo do quarto.

**RF010** O sistema deve permitir o registro dos profissionais de enfermaria contendo os dados: nome, CPF e registro no conselho de enfermagem (CRE).

## Diagrama ER
![ModeloHospital](https://github.com/Leuquary/hospital/assets/111248276/9a055889-724b-4a75-9798-adb8f42cadf0)

## Código SQL

```sql
create database hospital;
use hospital;

create table medico (
	codigo_medico int primary key,
	nome_medico varchar(50) not null,
	cpf_medico varchar(15) unique not null,
	rg_medico varchar(9) unique not null,
	cargo_medico varchar(20) not null, 
	data_nasc_medico date not null,
	codigo_especialidade int
);

create table paciente (
	codigo_paciente int primary key,
	nome_paciente varchar(50) not null,
	cpf_paciente varchar(11) unique not null, 
	rg_paciente varchar(9) unique not null, 
	telefone_paciente varchar(11) not null,
	email_paciente varchar(50) unique not null,
	data_nasc_paciente date not null,
	codigo_convenio int not null
);

create table convenio (
	numero_carteira int primary key, 
	nome_convenio varchar(50) not null,
	tempo_carencia varchar(10) not null,
	cnpj_convenio varchar(14) unique not null
);

create table consulta(
	codigo_consulta int primary key,
	data_consulta date not null,
	horario_consulta time not null,
	valor_consulta decimal(5,2) not null,
	forma_pagamento varchar(20) not null,
	codigo_paciente int not null,
	codigo_medico int not null, 
	codigo_especialidade int not null,
    codigo_convenio int
);

create table especialidade(
	codigo_especialidade int primary key,
	descricao_especialidade varchar(50) not null
);

create table receita(
	codigo_receita int primary key,
    nome_medicamento varchar(100) not null,
    instrucoes_medicamento varchar(255) not null,
    codigo_consulta int not null
);

create table endereco(
	codigo_endereco int primary key,
    rua varchar(100) not null,
    bairro varchar(100) not null,
    cep varchar(9) not null,
    numero int not null,
    complemento varchar(100),
    codigo_paciente int not null
);

create table internacao(
	codigo_internacao int primary key,
    data_prevista_alta date not null,
    data_entrada date not null,
    data_alta date,
    codigo_medico int not null,
    numero_quarto int not null
);

create table quarto(
	numero_quarto int primary key,
    codigo_tipo_quarto int not null
);

create table procedimento(
	codigo_procedimento int primary key,
    nome_procedimento varchar(50) not null,
    descricao_procedimento varchar(100) not null,
    codigo_internacao int not null
);

create table enfermeiro(
	codigo_enfermeiro int primary key,
    nome_enfermeito varchar(50) not null,
    rg_enfermeiro varchar(9) unique not null,
    cpf_enfermeiro varchar(15) unique not null,
	cre_enfermeiro varchar(20) unique not null,
    data_nasc_enfermeiro date not null
);

create table tipo_quarto(
	codigo_tipo_quarto int primary key,
    diaria_quarto decimal(5,2) not null,
    descricao_quarto varchar(200) not null
);

create table enfermeiro_internacao(
	codigo_enfermeiro int not null,
    codigo_internacao int not null
);

/*relacionando convenio e paciente*/
alter table paciente add foreign key fk_codigo_convenio (codigo_convenio) references convenio(numero_carteira);

/*relacionando especialidade e médico*/
alter table medico add foreign key fk_codigo_especialidade (codigo_especialidade) references especialidade(codigo_especialidade);

/*relacionando consulta e especialidade*/
alter table consulta add foreign key fk_codigo_especialidade (codigo_especialidade) references especialidade(codigo_especialidade);

/*relacionando médico e consulta*/
alter table consulta add foreign key fk_codigo_medico (codigo_medico) references medico(codigo_medico);

/*relacionando paciente e consulta*/
alter table consulta add foreign key fk_codigo_paciente (codigo_paciente) references paciente(codigo_paciente);

/*relacionando consulta e receita*/
alter table receita add foreign key fk_codigo_consulta (codigo_consulta) references consulta(codigo_consulta);

/*relacionando consulta e convenio*/
alter table consulta add foreign key fk_codigo_convenio (numero_carteira) references convenio(numero_carteira);

/*relacionando paciente e endereço*/
alter table endereco add foreign key fk_codigo_paciente (codigo_paciente) references paciente(codigo_paciente);

/*relacionando quarto e internação*/
alter table internacao add foreign key fk_numero_quarto (numero_quarto) references quarto(numero_quarto);

/*relacionando internção e procedimento*/
alter table procedimento add foreign key fk_codigo_internacao (codigo_internacao) references internacao(codigo_internacao);

/*relacionando internação e médico*/	
alter table internacao add foreign key fk_codigo_medico (codigo_medico) references medico(codigo_medico);

/*relacionando enfermeiro e internação*/
alter table enfermeiro_internacao add foreign key fk_codigo_enfermeiro (codigo_enfermeiro) references enfermeiro(codigo_enfermeiro);
alter table enfermeiro_internacao add foreign key fk_codigo_internacao (codigo_internacao) references internacao(codigo_internacao);

/*relacionando quarto e tipo*/
alter table quarto add foreign key fk_tipo_quarto (codigo_tipo_quarto) references tipo_quarto(codigo_tipo_quarto);
```

# O Prisioneiro dos Dados
Com o banco de dados para o sistema hospitalar completamente montado, é necessário incluir dados para realizar os devidos testes e validar sua viabilidade quanto ao sistema. Nesta etapa, também é importante realizar a separação de alguns scripts iniciais para o banco, com os dados que serão necessários a um povoamento inicial do sistema.

## Inclua ao menos dez médicos de diferentes especialidades. Ao menos sete especialidades (considere a afirmação de que “entre as especialidades há pediatria, clínica geral, gastrenterologia e dermatologia”).

```sql
insert into especialidade (codigo_especialidade, descricao_especialidade) values
(1, 'Cardiologia'),
(2, 'Pediatria'),
(3, 'Clínica geral'),
(4, 'Ortopedia'),
(5, 'Dermatologia'),
(6, 'Psiquiatria'),
(7, 'Ginecologia'),
(8, 'Oftalmologia'),
(9, 'Gastroenterologia'),
(10, 'Oncologia');

insert medico (codigo_medico, nome_medico, cpf_medico, rg_medico, cargo_medico, data_nasc_medico, codigo_especialidade) values
(1, 'Dr. João Silva', '123.456.789-00', 'MG1234567', 'Cardiologista', '1975-04-15', 1),
(2, 'Dra. Maria Souza', '234.567.890-11', 'SP2345678', 'Pediatra', '1980-06-20', 2),
(3, 'Dr. Carlos Pereira', '345.678.901-22', 'RJ3456789', 'Neurologista', '1978-09-10', 3),
(4, 'Dra. Ana Lima', '456.789.012-33', 'PR4567890', 'Ortopedista', '1985-11-25', 4),
(5, 'Dr. Paulo Gomes', '567.890.123-44', 'RS5678901', 'Dermatologista', '1970-12-30', 5),
(6, 'Dra. Fernanda Alves', '678.901.234-55', 'SC6789012', 'Psiquiatra', '1982-03-18', 6),
(7, 'Dr. Luiz Martins', '789.012.345-66', 'BA7890123', 'Ginecologista', '1973-07-22', 7),
(8, 'Dra. Helena Castro', '890.123.456-77', 'DF8901234', 'Oftalmologista', '1988-05-14', 8),
(9, 'Dr. Ricardo Santos', '901.234.567-88', 'CE9012345', 'Gastroenterologista', '1976-10-05', 9),
(10, 'Dra. Carolina Fernandes', '012.345.678-99', 'GO0123456', 'Oncologista', '1981-08-19', 10);
```

##Inclua ao menos 15 pacientes.
```sql
insert into convenio (numero_carteira, nome_convenio, tempo_carencia, cnpj_convenio) values
(1, 'Unimed', '30 dias', '11122233000101'),
(2, 'Amil', '60 dias', '22233344000202'),
(3, 'Bradesco Saúde', '45 dias', '33344455000303'),
(4, 'SulAmérica', '30 dias', '44455566000404'),
(5, 'Golden Cross', '60 dias', '55566677000505');

insert into paciente (codigo_paciente, nome_paciente, cpf_paciente, rg_paciente, telefone_paciente, email_paciente, data_nasc_paciente, codigo_convenio) values
(1, 'Alice Souza', '12345678901', 'MG1234567', '31987654321', 'alice@example.com', '1990-01-01', 1),
(2, 'Bruno Lima', '23456789012', 'SP2345678', '11987654322', 'bruno@example.com', '1985-02-02', 2),
(3, 'Carlos Pereira', '34567890123', 'RJ3456789', '21987654323', 'carlos@example.com', '1995-03-03', 3),
(4, 'Daniela Santos', '45678901234', 'PR4567890', '41987654324', 'daniela@example.com', '1980-04-04', 4),
(5, 'Eduardo Silva', '56789012345', 'RS5678901', '51987654325', 'eduardo@example.com', '1975-05-05', 5),
(6, 'Fernanda Oliveira', '67890123456', 'SC6789012', '61987654326', 'fernanda@example.com', '1988-06-06', 1),
(7, 'Gabriel Costa', '78901234567', 'BA7890123', '71987654327', 'gabriel@example.com', '1979-07-07', 2),
(8, 'Helena Martins', '89012345678', 'DF8901234', '81987654328', 'helena@example.com', '1992-08-08', 3),
(9, 'Igor Almeida', '90123456789', 'CE9012345', '91987654329', 'igor@example.com', '1983-09-09', 4),
(10, 'Julia Fernandes', '01234567890', 'GO0123456', '61987654330', 'julia@example.com', '1991-10-10', 5),
(11, 'Lucas Rocha', '12345098765', 'MA1234509', '71987654331', 'lucas@example.com', '1987-11-11', 1),
(12, 'Mariana Ribeiro', '23456109876', 'PA2345610', '81987654332', 'mariana@example.com', '1982-12-12', 2),
(13, 'Nicolas Lima', '34567210987', 'PE3456721', '91987654333', 'nicolas@example.com', '1993-01-13', 3),
(14, 'Olivia Silva', '45678321098', 'PI4567832', '61987654334', 'olivia@example.com', '1994-02-14', 4),
(15, 'Pedro Nunes', '56789432109', 'RJ5678943', '31987654335', 'pedro@example.com', '1990-03-15', 5);

insert into endereco (codigo_endereco, rua, bairro, cep, numero, complemento, codigo_paciente) values
(1, 'Rua A', 'Bairro A', '30123456', 101, 'Apto 1', 1),
(2, 'Rua B', 'Bairro B', '40123456', 102, 'Apto 2', 2),
(3, 'Rua C', 'Bairro C', '50123456', 103, 'Apto 3', 3),
(4, 'Rua D', 'Bairro D', '60123456', 104, 'Apto 4', 4),
(5, 'Rua E', 'Bairro E', '70123456', 105, 'Apto 5', 5),
(6, 'Rua F', 'Bairro F', '80123456', 106, 'Apto 6', 6),
(7, 'Rua G', 'Bairro G', '90123456', 107, 'Apto 7', 7),
(8, 'Rua H', 'Bairro H', '01123456', 108, 'Apto 8', 8),
(9, 'Rua I', 'Bairro I', '11123456', 109, 'Apto 9', 9),
(10, 'Rua J', 'Bairro J', '12123456', 110, 'Apto 10', 10),
(11, 'Rua K', 'Bairro K', '13123456', 111, 'Apto 11', 11),
(12, 'Rua L', 'Bairro L', '14123456', 112, 'Apto 12', 12),
(13, 'Rua M', 'Bairro M', '15123456', 113, 'Apto 13', 13),
(14, 'Rua N', 'Bairro N', '16123456', 114, 'Apto 14', 14),
(15, 'Rua O', 'Bairro O', '17123456', 115, 'Apto 15', 15);
```
