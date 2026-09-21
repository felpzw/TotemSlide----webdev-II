# Painel de Totens e Slides

Sistema web para gerenciamento de **totens de exibição** e **slides dinâmicos**, com atualização em tempo real via Socket.IO.

## ✨ Nome da proposta
**Painel de Totens e Slides**

## 📌 Funcionalidades
- Login de administrador.
- Cadastro e gerenciamento de totems.
- Geração de token de autenticação por totem.
- Cadastro, edição e exclusão de slides.
- Exibição de slides válidos (não expirados) na tela do totem.
- Atualização em tempo real dos slides para totems conectados.

## 🧱 Stack
- **Frontend:** Vue 3 + Vite
- **Backend:** Node.js + Express + Socket.IO
- **Banco:** MongoDB (Mongoose)
- **Infra local:** Docker Compose (MongoDB + Mongo Express)

## 📁 Estrutura do projeto
```text
.
├── backend
├── frontend
├── docker-compose.yaml
└── DOCUMENTACAO.md
```

## ⚙️ Pré-requisitos
- Node.js 20+
- npm
- Docker e Docker Compose (opcional, para MongoDB local)

## 🚀 Como executar
### 1) Subir banco de dados (opcional com Docker)
```bash
docker compose up -d
```

### 2) Configurar variáveis de ambiente do backend
No diretório `backend`, configure um arquivo `.env` com:
- `SERVER_PORT`
- `DB_HOST`
- `DB_PORT`
- `DB_NAME`
- `DB_USER`
- `DB_PASS`
- `DB_TOKEN_SECRET`

### 3) Instalar dependências
```bash
cd /home/runner/work/WebDev-Node-T2/WebDev-Node-T2/backend && npm install
cd /home/runner/work/WebDev-Node-T2/WebDev-Node-T2/frontend && npm install
```

### 4) Executar backend e frontend
Em terminais separados:
```bash
cd /home/runner/work/WebDev-Node-T2/WebDev-Node-T2/backend && npm run dev
cd /home/runner/work/WebDev-Node-T2/WebDev-Node-T2/frontend && npm run dev
```

## 🔌 Rotas principais
### Auth
- `POST /api/auth/signup`
- `POST /api/auth/login`
- `GET /api/auth/logoff`

### Slides (admin)
- `GET /api/slide`
- `POST /api/slide`
- `PUT /api/slide/:id`
- `DELETE /api/slide/:id`

### Totens (admin)
- `GET /api/totem`
- `POST /api/totem`
- `DELETE /api/totem/:id`

## 🖥️ Fluxo de uso (resumo)
1. Criar conta admin e realizar login.
2. Cadastrar totem e guardar o token gerado.
3. Cadastrar slides com tempo de duração e expiração.
4. Abrir rota `/totem` e informar token quando solicitado.
5. A tela do totem recebe atualizações automaticamente.

## 📚 Documentação complementar
Consulte `/home/runner/work/WebDev-Node-T2/WebDev-Node-T2/DOCUMENTACAO.md` para detalhes de arquitetura e funcionamento.
