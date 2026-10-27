# 🎫 ITSM Kanban — Multi-usuário

Board Kanban compartilhado para visualização de tickets do Intercom.
Todos os colegas veem o mesmo board em tempo real.

## Arquitetura

```
GitHub Pages (index.html) ──HTTPS──> Supabase (PostgreSQL + Real-time)
```

## Setup em 4 passos

### 1. Criar conta no Supabase (grátis)

1. Acesse [supabase.com](https://supabase.com) → **Start your project**
2. Crie um novo projeto (nome: `itsm-kanban`, senha forte)
3. Aguarde ~2 min para o banco inicializar

### 2. Criar as tabelas

1. No painel do Supabase → **SQL Editor** → **New query**
2. Cole o conteúdo do arquivo `setup.sql`
3. Clique em **Run** (▶)

### 3. Subir o app no GitHub Pages

```bash
git init
git add index.html setup.sql README.md
git commit -m "feat: ITSM Kanban multi-usuario"
gh repo create itsm-kanban --public --push --source=.
```

Em GitHub: **Settings → Pages → Branch: main → Save**
URL final: `https://SEU_USUARIO.github.io/itsm-kanban`

### 4. Configurar as credenciais (primeira vez)

1. Abra o app no browser
2. A tela de configuração aparece automaticamente
3. No Supabase: **Project Settings → API**
   - Copie `Project URL`
   - Copie `anon public` key
4. Cole no app → **Conectar**

A configuração fica salva no navegador de cada colega.
Cada pessoa faz isso uma vez ao abrir o app pela primeira vez.

## Como usar

| Ação | Como |
|------|------|
| Importar tickets | ⬆ Importar JSON → selecionar arquivo |
| Ver detalhes de um ticket | Clicar no card |
| Arquivar ticket resolvido | ✕ no card ou botão "Arquivar" no detalhe |
| Mover entre colunas | Arrastar o card |
| Buscar | Campo de busca no topo |
| Ver histórico | 📚 Histórico |
| Sincronização ao vivo | Automática — ponto verde = ao vivo |

## Lógica de importação

```
Para cada ticket do JSON:
  ├── ID já está no board?          → Ignorado
  ├── ID foi arquivado antes?       → ⚠ Aviso: "ticket voltou"
  ├── Título igual a arquivado?     → ⚠ Aviso: "problema recorrente"
  └── Completamente novo?           → ✅ Adicionado automaticamente
```

## Plano gratuito Supabase

| Recurso | Limite free |
|---------|-------------|
| Banco de dados | 500 MB |
| Usuários simultâneos | Ilimitado |
| Real-time | Incluído |
| Restrição | Projeto pausa após 1 semana sem uso |

> Para reativar: basta abrir o Supabase dashboard e clicar em "Restore".
