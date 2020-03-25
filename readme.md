# Semana OmniStack 11 

0. [Configuração de Ambiente:](#configuração-de-ambiente)
1. [Node.js](#nodejs-1)
2. [React.js](#reactjs)
3. [Rota e Recursos](#rota-e-recursos)
4. [Banco de dados](#banco-de-dados)

![alt text](/omniStack11.jpg)

----

## Configuração de Ambiente:

### Estrutura de diretórios
* `./backend`
    * `./scr`
    * `./database`
        * `./migration` 
* `./frontend`

### Visual Studio Code: Plugins (Ctrl+P)
    * ext install spywhere.guides
    * ext install eamodio.gitlens
    * ext install christian-kohler.path-intellisense
    * ext install vscode-icons-team.vscode-icons	

### Node.js
[Instalar o node.js](https://github.com/nodesource/distributions/blob/master/README.md)

* `npm`: instala um pacote
* `npx`: executa um pacote

~~~bash
 node -v #mostra a versão do node
 npm -v  #mostra a versão do npm
~~~

### Nodemon
* Atualiza automaticamente o servido do `Node.js`

~~~bash
npm install nodemon # em todo o programa
~~~

~~~bash
npm install nodemon -D # apenas na dependência de desenvolvimento
~~~

~~~bash
npm start # ativa e atualiza automaticamente o localhost:3333 
~~~

----

## Node.js

### Hello world

~~~bash
 mkdir backend
 cd backend
 npm init -y # incializando node.js
 npm install express # instalando micro-framework 'express' (configura rota e interpreta parâmetros)
 touch index.js 
~~~

* `request`: guarda todos os dados que são fornecidos da requisição do usuário
* `response`: responder todos os dados que são requisitados pelo usuário

~~~javascript
const express = require('express'); 

const app = express();

app.get('/',(request, response) => {
	return response.send('Hello World');
});

app.listen(3333);
~~~

~~~bash
 node index.js # ativa o localhost:3333
~~~

----

# Dia 2  // Parei em 00:34:13 

## Rota e Recursos

### Métodos HTTP
* `GET`: *Buscar/Listar* uma informação do back-end
* `POST`: *Cria* uma informação do back-end
* `PUT`: *Altera* uma informação do back-end
* `DELETE`: *Delete* uma informação do back-end

#### [Insomnia.rest](https://insomnia.rest/) : (Ferramenta para manipular os Métodos HTTP)
~~~bash 
$ sudo snap install insomnia 
~~~

#### Tipos de parâmetros
* `Query Params`: parâmetros nomeados enviados na rota após *"?"*. Exemplo: filtro, páginação;
* `Route Params`: parâmetros utilizados para identificar recursos ;
* `Request Body`: Corpo da requisição, utilizado para criar ou alterar recursos.
    * Converter json para javascript: `app.use(express.json());`.

---

## Banco de dados

### Modelo Conceitual: Entidades e Funcionalidades
* ONG
    * Cadastrar
    * Login
    * Logout
    * Contato
* CASOS (incident)
    * Cadastrar
    * Deletar
    * Listar
        * Especificos
        * Todos

### [SQLite](https://www.sqlite.org/index.html)
* Driver: SELECT * FROM users
* Query Builder: table('users').select( * ).where()

### [Knex.js](http://knexjs.org/)

* `Install`
~~~bash
npm install knex 
npm install sqlite3
~~~

~~~bash
npx knex init # configura o acesso ao banco de dados para cada aplicação
~~~

#### `Migrations` 

* Configuração do database pelo `knex`

~~~javascript
// knexfile.js
development: {
    client: 'sqlite3',
    connection: {
        filename: './src/database/db.sqlite'
    },
    migrations: {
        directory: './src/database/migrations'
    },
    useNullAsDefault: true
},
~~~

* gera uma tabela apenas no knexfile `create schema` 
~~~bash
npx knex migrate:make create_ongs 
~~~

* configura a estrutura da tabela para o comando `create table`
~~~javascript
// 20200325083011_create_ongs.js
exports.up = function(knex) {
  return knex.schema.createTable('ong', function (table) {
    table.string('id').primary();
    table.string('name').notNullable();
    table.string('email').notNullable();
    table.string('whatsapp').notNullable();
    table.string('city').notNullable();
    table.string('uf',2).notNullable();
  })
};

exports.down = function(knex) { return knex.schema.dropTable('ongs'); };
~~~

* executa o comando `create table` e cria tabela no banco de dados
~~~bash
npx knex migrate:latest 
~~~

* Desfaz o último comando do `npx knex migrate:latest`
~~~bash
npx knex migrate:rollback
~~~

---

## React.js - Frontend
~~~bash 
 npx create-react-app frontend #cria um projet
 cd frontend
 npm start
~~~