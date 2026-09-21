# DOCUMENTACAO — TotemSlide Hub

## 1. Visão geral
O **TotemSlide Hub** é um projeto acadêmico para gerenciamento e exibição de slides em totens digitais.

A solução é dividida em:
- **Frontend (Vue 3 + Vite)** para painel administrativo e tela do totem.
- **Backend (Node.js + Express + MongoDB)** para autenticação, CRUD de slides e totems.
- **Socket.IO** para atualização em tempo real dos slides exibidos nos totems.

---

## 2. Arquitetura

### 2.1 Frontend
Local: `/frontend`

Principais rotas:
- `/login` → autenticação de administrador
- `/admin` → painel principal
- `/admin/slides` → gerenciamento de slides
- `/admin/totems` → gerenciamento de totems
- `/totem` → tela pública do totem (consome slides em tempo real)

Views relevantes:
- `frontend/src/views/Login.vue`
- `frontend/src/views/Admin.vue`
- `frontend/src/views/ManageSlides.vue`
- `frontend/src/views/ManageTotens.vue`
- `frontend/src/views/Totem.vue`

### 2.2 Backend
Local: `/backend`

Servidor Express com endpoints:
- `/api/auth` → login, signup, logoff
- `/api/slide` → CRUD de slides (protegido)
- `/api/totem` → CRUD de totems (protegido)

A autenticação de admin é feita com JWT em:
- Header `Authorization` com esquema `Bearer`
- Ou cookie `token`

### 2.3 Tempo real com Socket.IO
- O totem conecta no socket enviando `token` do totem no `handshake.auth`.
- Ao conectar, recebe slides válidos pelo evento `update-slides`.
- Em criação/edição/remoção de slides no backend, o servidor faz broadcast de `update-slides` para todos os totems conectados.

---

## 3. Modelagem de dados (MongoDB)

### 3.1 Admin
Campos principais:
- `username` (único)
- `password` (hash com bcrypt)

### 3.2 Slide
Campos principais:
- `title` (único)
- `duration` (segundos)
- `content` (HTML)
- `expirationDate` (data de expiração)

### 3.3 Totem
Campos principais:
- `name`
- `authToken` (gerado no cadastro)
- `lastSeen`

---

## 4. Variáveis de ambiente
Arquivo usado atualmente: `backend/.env`

Variáveis esperadas:
- `DB_HOST`
- `DB_USER`
- `DB_PASS`
- `DB_NAME`
- `DB_PORT`
- `DB_TOKEN_SECRET`
- `SERVER_PORT`

> Recomendação acadêmica: usar valores locais para desenvolvimento e não reutilizar credenciais fora do ambiente de estudo.

---

## 5. Como executar o projeto

## 5.1 Pré-requisitos
- Node.js (versão compatível com frontend e backend)
- npm
- MongoDB local **ou** Docker

## 5.2 Subir banco com Docker (opcional)
Na raiz do projeto:

```bash
docker compose up -d
```

Isso sobe:
- MongoDB na porta `27017`
- Mongo Express na porta `8081`

## 5.3 Rodar backend
```bash
cd backend
npm install
npm run dev
```

Backend padrão em `http://localhost:4000` (dependendo de `SERVER_PORT`).

## 5.4 Rodar frontend
Em outro terminal:

```bash
cd frontend
npm install
npm run dev
```

O Vite exibirá a URL local (normalmente `http://localhost:5173`).

---

## 6. Fluxos principais

## 6.1 Administração
1. Criar conta admin (`/api/auth/signup`) ou usar uma já existente.
2. Fazer login em `/login`.
3. Acessar painel `/admin`.
4. Gerenciar slides e totems.

## 6.2 Totem
1. Cadastrar totem no painel de totems.
2. Copiar o `authToken` gerado.
3. Abrir rota `/totem` no dispositivo.
4. Informar token quando solicitado.
5. O totem recebe e atualiza slides automaticamente via socket.

---

## 7. Endpoints principais

### 7.1 Auth (`/api/auth`)
- `POST /signup`
- `POST /login`
- `GET /logoff`

### 7.2 Slides (`/api/slide`) — protegido por authAdmin
- `GET /`
- `POST /`
- `PUT /:id`
- `DELETE /:id`

### 7.3 Totems (`/api/totem`) — protegido por authAdmin
- `GET /`
- `POST /`
- `DELETE /:id`

---

## 8. Scripts

### Backend (`/backend/package.json`)
- `npm run dev` → inicia servidor Node (`app.js`)

### Frontend (`/frontend/package.json`)
- `npm run dev` → servidor de desenvolvimento Vite
- `npm run build` → build de produção
- `npm run preview` → preview local da build

---

## 9. Estrutura de diretórios

```text
WebDev-Node-T2/
├── backend/
│   ├── app.js
│   └── src/
│       ├── api/
│       │   ├── controllers/
│       │   ├── middleware/
│       │   ├── routes/
│       │   └── services/
│       ├── config/
│       └── models/
├── frontend/
│   ├── src/
│   │   ├── router/
│   │   └── views/
│   └── public/
└── docker-compose.yaml
```

---

## 10. Limitações e melhorias futuras
- Revisar internacionalização/consistência de idioma da interface.
- Adicionar testes automatizados (backend e frontend).
- Fortalecer validações de payload no backend.
- Evoluir autenticação de frontend para fluxo mais robusto (token/cookie sincronizado com sessão).
