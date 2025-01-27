# Vitrine de Medicamentos

## Descrição do Projeto
Este projeto consiste em uma API completa desenvolvida com **Node.js**, **TypeORM** e **PostgreSQL**.  
Seu objetivo principal é gerenciar informações de usuários e medicamentos, garantindo **segurança**, **validação** e uma estrutura **profissional**.

A aplicação permite que:
- Usuários se cadastrem.
- Façam login e autenticação segura.
- Registrem medicamentos que possuem em estoque.

## Funcionalidades
### Gerenciamento de Usuários
- Cadastro de usuários com hashing seguro de senhas (utilizando **bcrypt** ou similar).
- Autenticação de usuários com geração de tokens JWT.

### Gerenciamento de Medicamentos
- **CRUD completo**:
  - **Criar** medicamentos associados a usuários autenticados.
  - **Listar** medicamentos de forma geral ou por usuário.
  - **Atualizar** medicamentos (restrito ao criador).
  - **Excluir** medicamentos (restrito ao criador).
- Relacionamento entre medicamentos e usuários:
  - Cada medicamento pertence a um único usuário.
- Paginação e filtros:
  - Paginação configurada via `page` e `limit` nos endpoints de listagem.
  - Filtro por nome de medicamento nos endpoints de listagem.

## Tecnologias Utilizadas
- **Node.js** (back-end)
- **Express** (servidor web)
- **TypeORM** (ORM para manipulação de banco de dados)
- **PostgreSQL** (banco de dados relacional)
- **bcrypt** (hashing de senhas)
- **JWT** (autenticação baseada em tokens)

## Estrutura das Rotas

### Rotas de Usuários
- **POST /users**  
  Cadastra um novo usuário com os campos:  
  `nome`, `email`, e `senha` (armazenada como hash).
- **POST /login**  
  Autentica um usuário com base no `email` e `senha`.  
  Retorna um token JWT para acesso aos endpoints protegidos.

### Rotas de Medicamentos
- **POST /medicamentos**  
  Cria um novo medicamento associado ao usuário autenticado.  
  Campos: `nome`, `descricao` (opcional), `quantidade`.
- **GET /medicamentos/all**  
  Lista todos os medicamentos cadastrados no sistema, com paginação e filtro por `nome`.
- **GET /medicamentos**  
  Lista os medicamentos cadastrados pelo usuário autenticado, com paginação e filtro por `nome`.
- **GET /medicamentos/:id**  
  Retorna os detalhes de um medicamento específico.
- **PUT /medicamentos/:id**  
  Atualiza um medicamento específico.  
  **Somente o usuário criador pode realizar a atualização.**
- **DELETE /medicamentos/:id**  
  Remove um medicamento específico.  
  **Somente o usuário criador pode realizar a remoção.**

## Configuração do Projeto

```bash
# Clone o repositório
git clone https://github.com/SeuUsuario/vitrineMedicamentos.git
cd vitrineMedicamentos

# Instale as dependências
npm install

# Configure o banco de dados PostgreSQL no arquivo .env
# Exemplo:
DB_HOST=localhost
DB_PORT=5432
DB_USER=seu_usuario
DB_PASS=sua_senha
DB_NAME=vitrine_medicamentos

# Rode as migrações
npm run typeorm migration:run

# Inicie o servidor
npm start
