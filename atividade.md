
CREATE DATABASE colegio;

USE colegio;

CREATE TABLE Periodo (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(30)
);

INSERT INTO Periodo (nome) VALUES
('1° Turno - Manhã'),
('2° Turno - Tarde'),
('3° Turno - Noite');

CREATE TABLE Disciplina (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(30)
);

INSERT INTO Disciplina (nome) VALUES
('Programação Orientada'),
('Marketing Digital'),
('Banco de Dados'),
('Lógica'),
('Inglês Instrumental');

CREATE TABLE Professor (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(30),
    login varchar(10),
    senha varchar(10)
);

INSERT INTO Professor VALUES
(NULL, 'Aleandro', 'a@faex', '1234'),
(NULL, 'Marcus', 'm@faex', '2345'),
(NULL, 'Jonas', 'j@faex', '3456'),
(NULL, 'Rodrigo', 'r@faex', '4567'),
(NULL, 'Tamires', 't@faex', '6789');

CREATE TABLE Aluno (
    email_aluno VARCHAR(20) PRIMARY KEY,
    nome VARCHAR(30),
    senha VARCHAR(10),
    horario VARCHAR(10),
    horario_saida VARCHAR(10),
    curso int,
    periodo int
);

INSERT INTO Aluno VALUES
('Igor@faex', 'Igor', '1234', '19:30', '21:00', '1', '3'),
('Jose@faex', 'Jose', '2345', '21:00', '22:00', '5', '3'),
('Pedro@faex', 'Pedro', '3456', '20:40', '20:30', '3', '2'),
('Vinicius@faex', 'Vinicius', '4567', '19:00', '21:42', '1', '3'),
('Bruno@faex', 'Bruno', '5678', '20:20', '22:01', '2', '1'),
('Marcela@faex', 'Marcela', '8901', '20:32', '21:32', '4', '2'),
('Eduarda@faex', 'Eduarda', '9012', '21:11', '21:09', '2', '3'),
('Bebeto@faex', 'bebeto', '6789', '17:56', '19:58', '3', '2'),
('Roberto@faex', 'Roberto', '7890', '19:15', '20:55', '1', '1'),
('Jessica@faex', 'Jessica', '0123', '19:11', '22:09', '5', '1');


CREATE TABLE Provas (
    email_aluno VARCHAR(20) PRIMARY KEY,
    nota_1 VARCHAR(5),
    nota_2 VARCHAR(5)
);

INSERT INTO Provas VALUES
('Marcela@faex', '50', '30'),
('Igor@faex', '58', '65'),
('Jose@faex', '10', '38'),
('Pedro@faex', '25', '35'),
('Vinicius@faex', '62', '49'),
('Bruno@faex', '70', '57'),
('Jessica@faex', '50', '40'),
('Eduarda@faex', '65', '58'),
('Bebeto@faex', '49', '57'),
('Roberto@faex', '69', '60');

CREATE TABLE Stats (
    email_aluno VARCHAR(20) PRIMARY KEY,
    stats VARCHAR(15),
    presenca VARCHAR(10),
    provas_id INT
);


create view Resumo_Aluno as 

select 
a.email_aluno as A_email, 
a.horario,
a.horario_saida,
d.nome as nome_d,
p.nome as nome_p, 
pr.nome as nome_pr, 
pro.email_aluno 

from 
aluno a,
disciplina d,
periodo p,
professor pr,
provas pro

WHERE
a.email_aluno = pro.email_aluno and 
a.curso = d.id and 
a.periodo = p.id AND
d.id = pr.id

;

CREATE USER 'apenas_consulta'@'localhost' IDENTIFIED BY '123456';

GRANT SELECT ON colegio.resumo_aluno TO 'apenas_consulta'@'localhost';
