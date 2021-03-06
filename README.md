## Lemobs Test API 
![GitHub](https://img.shields.io/github/license/williamguilhermesouza/enderecosAlunosAPI)
![Repo-size](https://img.shields.io/github/repo-size/williamguilhermesouza/enderecosAlunosAPI)
![Last-commit](https://img.shields.io/github/last-commit/williamguilhermesouza/enderecosAlunosAPI)

This application was build during a test applied by lemobs, that had as goal to build a REST API
with NestJS and PostgreSQL DB. Also, the application docs where made using the swagger library, and 
can be acessed using the 'api' route. 

### How to use

First download the application code via git clone:

> $ git clone https://github.com/williamguilhermesouza/enderecosAlunosAPI.git

Install packages:

> $ yarn install

Then run the application (you must have the configured postgreSQL DB, see dbscripts):

> $ yarn start

## API information

The application is split between two main routes, as described below:

***
### **Alunos**

The alunos routes are basic CRUD operations in the database, where the routes are used to interact with the database, the routes are:

> **HOST:3000/aluno[GET]** : returns all alunos registered in the database

> **HOST:3000/aluno/media[GET]** : returns all alunos that have media greater than the average of all alunos notas.

> **HOST:3000/aluno/{nota}/criterio/{criterio}[GET]** : returns all alunos that have the register nota greater than the nota given if criterio is > (greater than) or alunos that have nota less than if criterio is <

> **HOST:3000/aluno/{id}[GET]** : returns the aluno that has the matching id 

> **HOST:3000/aluno/{id}[PUT]** : this route requires a json body, and updates the aluno registry with the given body

> **HOST:3000/aluno/{id}[DELETE]** : deletes the aluno with given id

> **HOST:3000/aluno[POST]** : creates the aluno using a json body
***
### **Enderecos**

The enderecos route uses only three routes as described:

> **HOST:3000/enderecos**[GET] : this route returns all enderecos at the database. It may be used a query param called bairro, that return only the bairro matching with the address register.

> **HOST:3000/enderecos**[POST] : this route uses a json body to create an endereco registry

> **HOST:3000/aluno/{id}/endereco**[GET] : this route returns all enderecos of the aluno with the matching id.

***

### Tables

For the application were used two tables in postgreSQL, which the scripts to create them can be found in the dbscripts folder, the tables have the structure described below:

#### Aluno
|Field | Value |
-------|--------|
id     | integer pk not null |
nome| string not null|
data_nascimento| timestamp not null|
cpf| string, not null|
nota| integer not null|

#### Endereco
|Field | Value |
-------|--------|
id| pk integer not null|
rua| string not null|
numero| varchar(5)|
complemento| string |
bairro| string not null|
aluno_id| fk integer not null|

***

Also, the application has a dockerfile and docker compose yml config file, and it can be built and run inside containers.

### GraphQL

Below, we have the above methods of the API mapped to the GraphQL:
#### **Alunos**

> **HOST:3000/aluno[GET]** : Alunos

> **HOST:3000/aluno/media[GET]** : approved 

> **HOST:3000/aluno/{nota}/criterio/{criterio}[GET]** : AlunoCriterio(nota, criterio)

> **HOST:3000/aluno/{id}[GET]** : Aluno(id)

> **HOST:3000/aluno/{id}[PUT]** : mutation updateAluno(id, aluno)

> **HOST:3000/aluno/{id}[DELETE]** : mutation deleteAluno(id)

> **HOST:3000/aluno[POST]** : mutation createAluno(aluno)
***
#### **Enderecos**

> **HOST:3000/enderecos**[GET] : Enderecos

> **HOST:3000/enderecos**[POST] : createEndereco(endereco)

> **HOST:3000/aluno/{id}/endereco**[GET] : AlunoResidencia(id)

***



#### CHANGELOG

|version| Modifications|
--------|--------------|
1.0| API construction|
1.1| Separation of DB access through DAO|
1.2| Creation of Unit and e2e test|
1.3| Implementation of Aluno and Endereco Services Interfaces|
1.4| Implementation of the API using GraphQL also keeping the original routes|

## AUTHOR: WILLIAM SOUZA
