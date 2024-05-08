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

