# 🗄️ Guia Simplificado - MongoDB Atlas

## Passo 1: Criar Conta

1. Acesse: https://www.mongodb.com/cloud/atlas/register
2. Você pode se registrar com:
   - ✅ Google (mais rápido)
   - ✅ GitHub
   - ✅ Email

3. Após login, você verá a tela inicial do Atlas

---

## Passo 2: Criar Database GRATUITO (M0)

### 2.1 Clique em "Create" ou "Build a Database"

Na tela inicial, procure o botão verde **"Create"** ou **"Build a Database"**

### 2.2 Escolha o Plano FREE

Você verá 3 opções de planos. Escolha:

```
┌─────────────────────────────┐
│  Shared                     │
│  FREE                       │  ← ESCOLHA ESTE
│  M0 Sandbox                 │
│  512 MB Storage             │
│  Shared RAM                 │
└─────────────────────────────┘
```

Clique em **"Create"** neste card

### 2.3 Configurar Região

```
Provider: AWS  (pode deixar)
Region:   South America (São Paulo) - sa-east-1  ← ESCOLHA BRASIL
Cluster Name: Cluster0  (pode deixar)
```

Clique em **"Create Cluster"**

⏳ Aguarde 1-3 minutos enquanto cria...

---

## Passo 3: Criar Usuário do Banco

Após criar, vai aparecer uma tela **"Security Quickstart"**

### 3.1 Criar Database User

```
Authentication Method: Username and Password

Username: animehub_admin
Password: [Clique em "Autogenerate Secure Password"]
```

**🔴 IMPORTANTE**: Clique em **"Copy"** e cole a senha em algum lugar seguro (bloco de notas)

Exemplo de senha gerada:
```
xK9mPqR2vN5tL8wE3fH7jS
```

Clique em **"Create User"**

---

## Passo 4: Liberar Acesso (Whitelist)

Ainda na mesma tela, mais abaixo:

### 4.1 Add IP Address

Você verá:
```
Where would you like to connect from?
```

Clique em **"Add My Current IP Address"** (adiciona seu IP atual)

**E TAMBÉM** clique em **"Add a Different IP Address"** e adicione:
```
IP Address: 0.0.0.0/0
Description: Allow all (for Railway/Vercel)
```

Clique em **"Add Entry"**

Por fim, clique em **"Finish and Close"**

---

## Passo 5: Obter String de Conexão

### 5.1 Ir para Connect

1. Vá em **"Database"** no menu lateral
2. Você verá seu cluster "Cluster0"
3. Clique no botão **"Connect"**

### 5.2 Escolher Método

Clique em **"Connect your application"**

### 5.3 Copiar Connection String

Você verá algo assim:

```
mongodb+srv://animehub_admin:<password>@cluster0.xxxxx.mongodb.net/?retryWrites=true&w=majority
```

**Clique em "Copy"**

### 5.4 Substituir <password>

Cole a string em um editor de texto e substitua `<password>` pela senha que você copiou no Passo 3.1

**ANTES:**
```
mongodb+srv://animehub_admin:<password>@cluster0.abc123.mongodb.net/?retryWrites=true&w=majority
```

**DEPOIS (exemplo):**
```
mongodb+srv://animehub_admin:xK9mPqR2vN5tL8wE3fH7jS@cluster0.abc123.mongodb.net/?retryWrites=true&w=majority
```

---

## ✅ Pronto! Você tem:

```
✓ Cluster MongoDB criado (Cluster0)
✓ Usuário criado (animehub_admin)
✓ Senha gerada (ex: xK9mPqR2vN5tL8wE3fH7jS)
✓ IP liberado (0.0.0.0/0)
✓ Connection String completa
```

---

## 📋 Copie e Guarde Estas Informações:

```bash
MONGODB_USERNAME=animehub_admin
MONGODB_PASSWORD=xK9mPqR2vN5tL8wE3fH7jS
MONGODB_URL=mongodb+srv://animehub_admin:xK9mPqR2vN5tL8wE3fH7jS@cluster0.abc123.mongodb.net/?retryWrites=true&w=majority
DATABASE_NAME=anime_tracker
```

**Você vai precisar da `MONGODB_URL` no Railway!**

---

## 🐛 Problemas Comuns

### ❌ "IP not whitelisted"
**Solução**: Volte em Network Access e adicione `0.0.0.0/0`

### ❌ "Authentication failed"
**Solução**: Verifique se substituiu `<password>` corretamente na string

### ❌ "Cannot connect to cluster"
**Solução**: Aguarde 2-3 minutos após criar o cluster

---

## ▶️ Próximo Passo

Agora que você tem o MongoDB configurado, vá para:

👉 **Deploy do Backend no Railway**

Siga o arquivo `DEPLOY.md` - Passo 2

Você vai usar a `MONGODB_URL` que você acabou de criar!
