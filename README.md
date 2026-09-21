# TotemSlide Hub

Projeto acadêmico para gerenciamento e transmissão de slides para totems digitais com atualização em tempo real.

## Objetivo
Permitir que um administrador:
- faça login no painel;
- cadastre e gerencie slides;
- cadastre totems e distribua tokens de acesso;
- publique atualizações que aparecem automaticamente nos totems conectados.

## Tecnologias
- **Frontend:** Vue 3, Vue Router, Vite, Socket.IO Client
- **Backend:** Node.js, Express, Socket.IO, JWT, Bcrypt
- **Banco:** MongoDB (com opção de Docker Compose)

## Estrutura
- `/frontend` → interface web (admin + totem)
- `/backend` → API, autenticação e integração com MongoDB
- `docker-compose.yaml` → apoio para subir MongoDB localmente

## Execução rápida
### 1) Banco (opcional via Docker)
```bash
docker compose up -d
```

### 2) Backend
```bash
cd backend
npm install
npm run dev
```

### 3) Frontend
```bash
cd frontend
npm install
npm run dev
```

## Rotas da aplicação
- `/login` → login administrativo
- `/admin` → painel
- `/admin/slides` → gestão de slides
- `/admin/totems` → gestão de totems
- `/totem` → tela do totem

## Documentação completa
Consulte o arquivo [`DOCUMENTACAO.md`](./DOCUMENTACAO.md) para detalhes de arquitetura, modelos, APIs e fluxo completo do projeto.

## Contexto acadêmico
Este projeto foi desenvolvido para fins educacionais, com foco em integração entre frontend/backend, autenticação, persistência em MongoDB e comunicação em tempo real com Socket.IO.
