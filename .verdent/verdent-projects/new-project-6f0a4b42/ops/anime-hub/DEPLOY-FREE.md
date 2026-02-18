# 🚀 Deploy GRATUITO - Sem Cartão de Crédito

## Alternativa 1: Railway com PostgreSQL (100% FREE)

Railway oferece $5 de crédito mensal grátis + PostgreSQL incluído!

### Passo 1: Criar Conta no Railway

1. Acesse: https://railway.app
2. Clique em **"Login"**
3. Escolha **"Login with GitHub"**
4. Autorize o Railway
5. ✅ Você ganha $5/mês automaticamente (sem cartão!)

---

### Passo 2: Criar Novo Projeto

1. Na dashboard, clique em **"New Project"**
2. Escolha **"Deploy from GitHub repo"**
3. Selecione `migueleng-dev/anime-hub`
4. Railway vai detectar automaticamente

---

### Passo 3: Adicionar PostgreSQL (Grátis)

1. No projeto, clique em **"+ New"**
2. Escolha **"Database"**
3. Selecione **"Add PostgreSQL"**
4. Aguarde 30 segundos
5. ✅ PostgreSQL criado!

---

### Passo 4: Configurar Backend

1. Clique no serviço do **backend**
2. Vá em **"Settings"**
3. Configure:

```
Root Directory: backend
Build Command: pip install -r requirements.txt
Start Command: uvicorn server:app --host 0.0.0.0 --port $PORT
```

4. Vá em **"Variables"**
5. Clique em **"+ New Variable"** e adicione:

```bash
PYTHON_VERSION=3.11.0
JWT_SECRET=seu-secret-aleatorio-min-32-caracteres-aqui
CORS_ORIGINS=*
```

6. O Railway automaticamente criará a variável `DATABASE_URL` do PostgreSQL!

---

### Passo 5: Deploy

1. Clique em **"Deploy"**
2. Aguarde 2-3 minutos
3. Vá em **"Settings"** → **"Networking"**
4. Clique em **"Generate Domain"**
5. ✅ Copie a URL: `https://anime-hub-backend.up.railway.app`

---

## Alternativa 2: Vercel + Vercel Postgres (100% FREE)

### Passo 1: Deploy no Vercel

1. Acesse: https://vercel.com
2. Login com GitHub
3. **"Add New..."** → **"Project"**
4. Selecione `migueleng-dev/anime-hub`
5. Configure:
   - Root Directory: `frontend`
   - Build Command: `yarn build`

### Passo 2: Adicionar Postgres (Storage - Free)

1. No dashboard do projeto, vá em **"Storage"**
2. Clique em **"Create Database"**
3. Escolha **"Postgres"**
4. Nome: `anime-hub-db`
5. Clique em **"Create"**
6. ✅ Grátis para sempre!

### Passo 3: Backend no Vercel Serverless

Para o backend, vamos usar Vercel Serverless Functions!

---

## ⭐ Recomendação: Railway (Mais Fácil)

Railway é a opção **MAIS SIMPLES** porque:

- ✅ Sem cartão de crédito
- ✅ $5 crédito mensal grátis
- ✅ PostgreSQL incluído grátis
- ✅ Deploy automático do GitHub
- ✅ SSL/HTTPS automático
- ✅ Logs em tempo real

---

## 📊 Comparação

| Plataforma | Banco | Crédito/Mês | Cartão? |
|------------|-------|-------------|---------|
| Railway | PostgreSQL | $5 | ❌ Não |
| Render | PostgreSQL | 90 dias | ❌ Não |
| MongoDB Atlas | MongoDB | Grátis | ⚠️ Depende |
| Vercel + Supabase | PostgreSQL | Grátis | ❌ Não |

---

## 🎯 Escolha Rápida

### Para INICIAR AGORA (5 minutos):
👉 **Railway** (mais simples)

### Para ESCALAR depois:
👉 **Vercel + Supabase**

---

## 🆘 Precisa de Ajuda?

Me diga qual opção você prefere e eu te ajudo passo a passo!

1️⃣ Railway (recomendado - mais fácil)
2️⃣ Vercel + Supabase
3️⃣ Render + PostgreSQL
