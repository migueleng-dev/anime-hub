# 🚀 Guia de Deploy - AnimeHub

Este guia te ajudará a fazer deploy completo do AnimeHub com URLs permanentes gratuitas.

## 📋 Pré-requisitos

1. Conta no [GitHub](https://github.com) (você já tem!)
2. Conta no [Vercel](https://vercel.com) (gratuita)
3. Conta no [Railway](https://railway.app) (gratuita - $5 crédito inicial)
4. Conta no [MongoDB Atlas](https://mongodb.com/cloud/atlas) (gratuita)

---

## 🗄️ Passo 1: Configurar MongoDB Atlas (Banco de Dados)

### 1.1 Criar Cluster Gratuito

1. Acesse [MongoDB Atlas](https://www.mongodb.com/cloud/atlas/register)
2. Crie uma conta ou faça login
3. Clique em **"Build a Database"**
4. Escolha **"M0 FREE"** (Shared)
5. Selecione região mais próxima (ex: São Paulo - sa-east-1)
6. Clique em **"Create"**

### 1.2 Configurar Acesso

1. **Database Access** (usuário):
   - Clique em **"Database Access"** no menu lateral
   - **"Add New Database User"**
   - Username: `animehub_user`
   - Password: Gere uma senha forte e **SALVE**
   - Database User Privileges: `Read and write to any database`
   - Clique em **"Add User"**

2. **Network Access** (liberar IP):
   - Clique em **"Network Access"**
   - **"Add IP Address"**
   - Clique em **"Allow Access from Anywhere"** (0.0.0.0/0)
   - Clique em **"Confirm"**

### 1.3 Obter Connection String

1. Vá em **"Database"** → **"Connect"**
2. Escolha **"Connect your application"**
3. Copie a string de conexão:
   ```
   mongodb+srv://animehub_user:<password>@cluster0.xxxxx.mongodb.net/?retryWrites=true&w=majority
   ```
4. Substitua `<password>` pela senha que você criou
5. **GUARDE ESSA STRING** - você vai precisar nos próximos passos

---

## 🔧 Passo 2: Deploy do Backend (Railway)

### 2.1 Criar Projeto no Railway

1. Acesse [Railway](https://railway.app)
2. Faça login com GitHub
3. Clique em **"New Project"**
4. Escolha **"Deploy from GitHub repo"**
5. Selecione o repositório `migueleng-dev/anime-hub`
6. Railway detectará automaticamente o projeto

### 2.2 Configurar Variáveis de Ambiente

1. Selecione o serviço do backend
2. Vá na aba **"Variables"**
3. Adicione as seguintes variáveis:

```bash
MONGO_URL=mongodb+srv://animehub_user:SUA_SENHA@cluster0.xxxxx.mongodb.net/?retryWrites=true&w=majority
DB_NAME=anime_tracker
JWT_SECRET=gere-uma-string-aleatoria-segura-aqui-min-32-chars
CORS_ORIGINS=*
PYTHON_VERSION=3.11.0
```

> **Importante**: Para `JWT_SECRET`, gere uma string aleatória longa (mínimo 32 caracteres). Você pode usar: https://www.random.org/strings/

### 2.3 Configurar Deploy do Backend

1. Vá em **"Settings"**
2. Em **"Root Directory"**, configure: `backend`
3. Em **"Build Command"**, configure: `pip install -r requirements.txt`
4. Em **"Start Command"**, configure: `uvicorn server:app --host 0.0.0.0 --port $PORT`
5. Em **"Health Check Path"**, configure: `/health`
6. Clique em **"Deploy"**

### 2.4 Obter URL do Backend

1. Após o deploy, vá em **"Settings"** → **"Networking"**
2. Clique em **"Generate Domain"**
3. Você receberá uma URL tipo: `https://anime-hub-backend-production.up.railway.app`
4. **COPIE ESSA URL** - você vai usar no frontend

---

## 🎨 Passo 3: Deploy do Frontend (Vercel)

### 3.1 Importar Projeto

1. Acesse [Vercel](https://vercel.com)
2. Faça login com GitHub
3. Clique em **"Add New..."** → **"Project"**
4. Selecione `migueleng-dev/anime-hub`
5. Clique em **"Import"**

### 3.2 Configurar Build Settings

1. **Framework Preset**: `Create React App`
2. **Root Directory**: `frontend`
3. **Build Command**: `yarn build` (padrão)
4. **Output Directory**: `build` (padrão)

### 3.3 Configurar Variáveis de Ambiente

Na seção **"Environment Variables"**, adicione:

```bash
REACT_APP_BACKEND_URL=https://anime-hub-backend-production.up.railway.app
```

> **Substitua pela URL do seu backend do Railway** (sem "/" no final)

### 3.4 Deploy

1. Clique em **"Deploy"**
2. Aguarde o build (2-3 minutos)
3. Você receberá uma URL tipo: `https://anime-hub-xxx.vercel.app`

### 3.5 Configurar Domínio Personalizado (Opcional)

1. Vá em **"Settings"** → **"Domains"**
2. Adicione seu domínio customizado se tiver
3. Ou use o domínio `.vercel.app` fornecido gratuitamente

---

## 🔐 Passo 4: Atualizar CORS no Backend

Agora que você tem a URL do frontend, vamos atualizar o CORS:

1. Volte ao Railway
2. Edite a variável `CORS_ORIGINS`:
   ```
   CORS_ORIGINS=https://anime-hub-xxx.vercel.app,http://localhost:3000
   ```
3. Salve e aguarde o redeploy automático

---

## ✅ Passo 5: Testar a Aplicação

1. Acesse a URL do Vercel: `https://anime-hub-xxx.vercel.app`
2. Registre uma nova conta
3. Faça login
4. Explore animes e adicione favoritos
5. Verifique se tudo funciona!

---

## 📊 Monitoramento

### Railway (Backend)
- **Logs**: Aba "Deployments" → clique no deploy → "View Logs"
- **Métricas**: Aba "Metrics" (CPU, RAM, requests)
- **Health**: Acesse `https://sua-url-backend.railway.app/health`

### Vercel (Frontend)
- **Analytics**: Aba "Analytics" (visitantes, performance)
- **Logs**: Aba "Deployments" → clique no deploy → "View Function Logs"

### MongoDB Atlas
- **Monitoring**: Aba "Metrics" (connections, operations)
- **Database**: Aba "Collections" (visualizar dados)

---

## 🆓 Limites do Plano Gratuito

### MongoDB Atlas M0 (Free)
- ✅ 512 MB de armazenamento
- ✅ Shared RAM e CPU
- ✅ Ideal para projetos pequenos/médios

### Railway (Hobby)
- ✅ $5 de crédito mensal gratuito
- ✅ ~500 horas de execução
- ✅ 100GB de tráfego

### Vercel (Hobby)
- ✅ 100GB de bandwidth
- ✅ 100 builds/mês
- ✅ Domínio .vercel.app gratuito

---

## 🔄 Deploy Automático (CI/CD)

Já configurado! Sempre que você fizer push para `master`:

- ✅ **Frontend**: Vercel rebuilda automaticamente
- ✅ **Backend**: Railway rebuilda automaticamente

---

## 🐛 Troubleshooting

### Frontend não conecta ao Backend

1. Verifique `REACT_APP_BACKEND_URL` no Vercel
2. Certifique-se que não tem `/` no final
3. Teste a URL do backend: `https://sua-url/health`

### Erro de CORS

1. Verifique `CORS_ORIGINS` no Railway
2. Adicione a URL completa do Vercel
3. Aguarde o redeploy

### Erro de Conexão MongoDB

1. Verifique se liberou 0.0.0.0/0 no Network Access
2. Confirme usuário e senha em `MONGO_URL`
3. Teste a conexão com MongoDB Compass

### Backend não inicia

1. Verifique logs no Railway
2. Confirme que todas as variáveis de ambiente estão corretas
3. Teste localmente: `uvicorn server:app --reload`

---

## 🎉 Parabéns!

Seu AnimeHub está no ar com URLs permanentes:

- 🌐 **Frontend**: `https://anime-hub-xxx.vercel.app`
- 🔧 **Backend**: `https://anime-hub-backend-xxx.railway.app`
- 🗄️ **Database**: MongoDB Atlas

### Próximos Passos (Opcional)

- [ ] Adicionar domínio customizado (ex: `animehub.com.br`)
- [ ] Configurar Google Analytics
- [ ] Adicionar Sentry para monitoramento de erros
- [ ] Implementar cache com Redis
- [ ] Adicionar testes E2E com Cypress

---

## 📞 Suporte

Encontrou algum problema? Abra uma issue:
https://github.com/migueleng-dev/anime-hub/issues

---

**Desenvolvido por Miguel Angelo** 🚀
