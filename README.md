# Projeto-Integrador-2021
Trabalho escolar com ênfase na área médica realizado pelos alunos Emanuel Lázaro, Estéfano Santos e Estêvão Turbay
 
Link do texto mais explicativo:

https://docs.google.com/document/d/1mC07AvuXS8oQGCfKQ_-hxKqqsdLu0tGZfcwPvgP_K0g/edit?usp=sharing


Organização do Projeto até o momento(atualizado): 

Emanuel Lázaro realizou as atividades 1, 2  e auxiliou na 6 e 8 além da 10;
Estêvão realizou as tarefas 3, 4 e auxiliou na 7, e 9;
Estéfano realizou as tarefas 5, além da 6, 7 e 8, 9 e 10 com ajuda dos demais participantes do projeto; envio das tarefas para o ava.

Componentes:
Estêvão: estevaoturbay@gmail.com 
Estéfano: estefanosb@gmail.com 
Emanuel emanuellalazaro@gmail.com

Minimundo:

O aplicativo contará com 3 telas principais, as quais subdividem-se nas áreas citadas abaixo. Ao adentrar o programa, o utilizador verá uma parte de registro, onde haverá um corpo humano, no qual o usuário pode usar de referência para saber onde seus problemas de saúde estão ocorrendo, além de mais informações sobre sua atual doença, como os sintomas, sua temperatura corporal, a intensidade e local das dores, entre outros problemas. 
Na aba relatório se situarão as anotações anteriores, armazenadas em ordem cronológica, facilitando a lembrança dos problemas de saúde anteriores do utilizador.
Já na parte da ficha médica, teremos todos os dados de saúde relacionados ao usuário. Desde possíveis comorbidades, alergias a medicamentos, deficiências, tipo sanguíneo até características pessoais, tais como estatura, número de documentos de identificação, massa corporal, gênero, incluindo também formas de contato de algum familiar ou responsável em caso emergencial.

Mockup:

No mockup, haverá 3 telas navegáveis pelo usuário, as quais podem ser acessadas e trocadas através de movimentos laterias do usuário (foto exemplo no link acima)

Os alunos que estão desenvolvendo o projeto são: Emanuel Lázaro Silva Ribeiro, Estéfano Santos Binda e Estêvão Turbay de Lyra. O projeto tem por finalidade facilitar o armazenamento e disposição de informações relacionadas à saúde pessoal do usuário.

Tabela: 

https://docs.google.com/spreadsheets/d/1Blu3Pv9xKuRV-hMeaNiL2HGNnXMQ81Amn78C9mi3JmM/edit?usp=sharing

PMC:

O pmc com dados como justificatica, premissas, riscos etc encontra-se no link do arquivo google docs

Modelo Conceitual:

Feito no BrModelo, há quatro tabelas e diveros atributos. A tabela pessoa possui as credenciais principais quanto ao usuário, enquanto a tabela dados de saúde armazena características mais específicas e que podem ser variadas ao passar do tempo. Se uma ocorrer para o utilizador algum problema de saúde, ficará registrado na tabela Ocorrência, descrevendo detalhadamente aquilo que aconteceu (sintomas, horário, local etc). Por fim, a tabela Tratamento servirá para auxiliar o usuário em sua recuperação, após uma consulta com um profissional de saúde devidamente qualificado, com a descrição de seu tratamento assim como a informação de qual problema de saúde ele veio a ter.

Modelo lógico pode ser visto no link acima;

Modelo físico:

8. e 9. Modelo Físico e Inserts

DROP SCHEMA IF EXISTS Projeto_integrador ;
CREATE SCHEMA IF NOT EXISTS Projeto_integrador DEFAULT CHARACTER SET utf8 COLLATE utf8_general_ci;
USE Projeto_integrador ;

CREATE TABLE Pessoa (
  CPF_user VARCHAR(50) NOT NULL,
  Nome VARCHAR(50) NOT NULL,
  Idade INT NOT NULL,
  Sexo CHAR NOT NULL,
  PRIMARY KEY (CPF_user));
  
CREATE TABLE Dados (
  CPF_user VARCHAR(50) NOT NULL,
  Tipo_sanguineo VARCHAR(10) NOT NULL ,
  Contato_Emergencia VARCHAR(20) DEFAULT NULL ,
  Alergias_Comorbidades VARCHAR(100) DEFAULT NULL ,
  PRIMARY KEY (Tipo_sanguineo),
  CONSTRAINT fk_Dados_Pessoa1
    FOREIGN KEY (CPF_user)
    REFERENCES Pessoa (CPF_user)
	ON DELETE NO ACTION
    ON UPDATE NO ACTION);

CREATE TABLE Ocorrencia (
  CPF_user VARCHAR(50) NOT NULL,
  Num_caso INT NOT NULL ,
  Sintomas VARCHAR(200) NOT NULL ,
  Local_data VARCHAR(100) NOT NULL ,
  PRIMARY KEY (Num_caso),
  CONSTRAINT fk_Ocorrencia_Pessoa1
    FOREIGN KEY (CPF_user)
    REFERENCES Pessoa (CPF_user)
	ON DELETE NO ACTION
    ON UPDATE NO ACTION);
    
CREATE TABLE Tratamento (
  Num_caso INT NOT NULL ,
  Dsc_tratamento VARCHAR(100) DEFAULT NULL ,
  Problema_saude VARCHAR(100) NOT NULL ,
  PRIMARY KEY (Problema_saude),
  CONSTRAINT fk_Tratamento_Ocorrencia1
    FOREIGN KEY (Num_caso)
    REFERENCES Ocorrencia (Num_caso)
	ON DELETE NO ACTION
    ON UPDATE NO ACTION);
        
INSERT INTO Pessoa (CPF_user, Nome, Idade, Sexo) VALUES 
('12345678910','Joao Silva', 40, "M"),
('23456789012','Josefina Maria','50',"F");



INSERT INTO Dados (CPF_user, Tipo_sanguineo, Contato_Emergencia, Alergias_Comorbidades) VALUES 
('12345678910','O+', "2799999999", NULL),
('23456789012','AB-','2798888888',"Dipirona");



INSERT INTO Ocorrencia (CPF_user, Num_caso, Sintomas, Local_data) VALUES 
('12345678910','1', "dermatites e febre", "18 de janeiro 2021 em casa (Vitoria)"),
('12345678910','2', "diarreia, prisao de ventre", "6 de fevereiro de 2021 no sitio(Ecoporanga)" ),
('12345678910','3', "dores articulares, febre alta", "21 de fevereiro de 2021 em casa (Vitoria)"),
('23456789012','4','dor articular, calafrio, náuseas',"6 de marco de 2021 na zona rural de Viana"),
('23456789012','5','manchas vermelhas, coceira',"10 de abirl de 2021 em casa (Vila Velha)"),
('23456789012','6','dores atras dos olhos, perda de apetite',"2 de maio de 2021 numa viagem (Natal)");


INSERT INTO Tratamento (Num_caso, Dsc_tratamento, Problema_saude ) VALUES 
('1', "antiparasitários 1x dia", "esquistossomose"),
('2', "antiparasitarios 2x dia", "teníase" ),
('3', "analgesicos e ingestao de liquidos", "dengue"),
('4','líquidos intravenosos, reidratação oral',"chikungunya"),
('5','Analgésicos, repouso por 14 dias',"catapora"),
('6','antitermicos e analgésicos',"zika vírus");



10. Prints das consultas das tabelas foram enviadas por pdf no ava 
