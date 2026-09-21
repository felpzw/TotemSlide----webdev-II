# Painel de Totens e Slides

## 1. Visão geral
O **Painel de Totens e Slides** é uma aplicação web para cadastro e gerenciamento de totems de exibição e de slides em HTML, com atualização em tempo real para dispositivos conectados.

## 2. Objetivo da proposta
Centralizar a administração de conteúdo exibido em telas públicas (totens), permitindo:
- autenticação de administradores;
- cadastro de dispositivos totem com token de acesso;
- criação, edição e remoção de slides;
- distribuição automática de slides válidos para os totems conectados.

## 3. Arquitetura do projeto
- **Frontend:** Vue 3 + Vite + Vue Router (`/frontend`)
- **Backend:** Node.js + Express + Socket.IO (`/backend`)
- **Banco de dados:** MongoDB
- **Orquestração auxiliar:** Docker Compose (MongoDB + Mongo Express)

## 4. Funcionalidades principais
### 4.1 Administração
- Login e logout de administrador.
- Controle de acesso às rotas administrativas.

### 4.2 Gestão de slides
- Listagem de slides cadastrados.
- Criação, edição e exclusão de slides.
- Campos principais do slide:
  - título;
  - duração em segundos;
  - conteúdo HTML;
  - data de expiração.

### 4.3 Gestão de totems
- Cadastro de novos totems.
- Geração de token único por totem.
- Listagem com informações de criação e último acesso.
- Remoção de totems.

### 4.4 Exibição em totem
- Conexão via Socket.IO autenticada por token do totem.
- Recebimento dos slides válidos (não expirados).
- Atualização em tempo real quando slides são alterados no painel.

## 5. APIs e comunicação
### 5.1 Rotas HTTP (prefixo `/api`)
- **Auth** (`/auth`)
  - `POST /signup`
  - `POST /login`
  - `GET /logoff`
- **Slides** (`/slide`) *(requer autenticação de admin)*
  - `GET /`
  - `POST /`
  - `PUT /:id`
  - `DELETE /:id`
- **Totens** (`/totem`) *(requer autenticação de admin)*
  - `GET /`
  - `POST /`
  - `DELETE /:id`

### 5.2 Socket.IO
- Middleware de autenticação por `socket.handshake.auth.token`.
- Evento enviado pelo backend para clientes totem:
  - `update-slides`

## 6. Segurança e autenticação
- Senhas de admin com hash (`bcrypt`).
- Sessão de admin com JWT em cookie `httpOnly`.
- Endpoints administrativos protegidos por middleware de autenticação.
- Totens autenticados por token exclusivo.

## 7. Estrutura de diretórios (resumo)
- `/backend`: API, regras de negócio, modelos e Socket.IO.
- `/frontend`: interface administrativa e tela de totem.
- `docker-compose.yaml`: serviços de suporte para MongoDB.

## 8. Estado atual e próximos passos sugeridos
- Padronizar idioma e textos da interface (PT-BR).
- Criar arquivo de ambiente de exemplo (`.env.example`) no backend.
- Adicionar testes automatizados para serviços e rotas críticas.
- Melhorar observabilidade (logs e tratamento de erros em produção).
