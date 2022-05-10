# Backend da aplicação Tasks

Backend do aplicativo *To-Do List* [Task](https://github.com/fabioTowers/tasks) para registro e acompanhamento de tarefas.

Desenvolvido com [NodeJS](https://nodejs.org/en/about/) esse aplicativo utiliza a arquitetura API REST para se comunicar com a aplicação mobile no frontend.

Para acessar determinados endpoints há o controle de acesso utilizando token JWT para autenticação dos usuários.

### Endpoints da aplicação

- `/signup` (POST): Registrar usuário;
- `/signin` (POST): Autenticar usuário (utilizando Token JWT);
- `/tasks`:
    - `GET`: Recuperar a lista das tarefas cadastradas pelo usuário;
    - `POST`: Salvar uma nova tarefa;
- `/tasks/:id` (DELETE): remove uma tarefa de um usuário de acordo com o ID;
- `/tasks/:id/toggle` (PUT): Muda o estado de uma task para concluída.

### Instruções de deploy

1. Instalar o knex:
```batch
npm i knex -g
```

2. Criar o arquivo knexfile.js na raiz do projeto com o seguinte conteúdo:
```javascript
/**
 * @type { Object.<string, import("knex").Knex.Config> }
 */
module.exports = {
  client: 'postgresql',
  connection: {
    database: 'schema_name',
    user:     'user',
    password: 'password'
  },
  pool: {
    min: 2,
    max: 10
  },
  migrations: {
    tableName: 'knex_migrations'
  }
};
```

3. Executar as migrations:

```batch
knex migrate:latest
```

4. Criar o arquivo .env na raiz do projeto e inserir uma chave de autenticação para os tokens JWT, conteúdo do arquivo:

```
module.exports = {
    authSecret: ''
}
```

**Executar a aplicação**: `npm start`