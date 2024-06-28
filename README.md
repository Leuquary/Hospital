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

Código SQL

```sql
create database hospital;
use hospital;

create table medico (
	codigo_medico int primary key,
	nome_medico varchar(50) not null,
	cpf_medico varchar(14) unique not null,
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
    cpf_enfermeiro varchar(14) unique not null,
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
