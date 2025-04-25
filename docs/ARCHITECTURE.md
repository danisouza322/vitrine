# Arquitetura do Projeto Vitrine

## Visão Geral
O Vitrine é uma aplicação web que permite usuários encontrarem produtos disponíveis em diferentes cidades. A aplicação utiliza Next.js para o frontend e Supabase como backend.

## Estrutura do Projeto

```
vitrine/
├── src/
│   ├── app/
│   │   ├── [cidade]/
│   │   │   └── page.tsx      # Página específica da cidade
│   │   └── page.tsx          # Página principal
│   ├── components/
│   │   └── ui/              # Componentes de UI
│   └── lib/
│       └── db/
│           ├── index.ts      # Configuração do Supabase
│           ├── schema.ts     # Schema do banco de dados
│           └── utils.ts      # Funções de utilidade para DB
```

## Componentes Principais

### 1. Página Principal (`src/app/page.tsx`)
- Renderiza a lista de cidades disponíveis
- Implementa tratamento de erros
- Usa o componente de navegação comum
- Fornece link para área administrativa

### 2. Página da Cidade (`src/app/[cidade]/page.tsx`)
- Renderiza produtos específicos da cidade
- Implementa navegação e filtros
- Mostra informações detalhadas dos produtos
- Possui botão de contato via WhatsApp

## Banco de Dados

### Tabelas Principais
1. `cidades`
   - id: string (UUID)
   - nome: string
   - slug: string
   - created_at: timestamp

2. `lojas`
   - id: string (UUID)
   - nome: string
   - slug: string
   - cidade_id: string (FK)

3. `produtos`
   - id: string (UUID)
   - nome: string
   - preco: number
   - loja_id: string (FK)

## Funcionalidades Implementadas

### Sistema de Cache
- Cache em memória para cidades
- Duração: 5 minutos
- Implementado em `utils.ts`

### Otimizações Realizadas
1. Query otimizada para cidades:
   - Seleção específica de campos
   - Ordenação por nome
   - Validação de dados
   - Logs estruturados

### Tratamento de Erros
- Logs detalhados com contexto
- Tratamento de casos nulos
- Respostas apropriadas para o usuário

## Decisões Técnicas

### 1. Uso do Supabase
- Escolhido pela facilidade de implementação
- Oferece autenticação integrada
- Bom suporte a tempo real

### 2. Cache em Memória
- Implementado para reduzir carga no banco
- Balanceamento entre performance e consistência
- Tempo de expiração configurável

### 3. Tipagem Forte
- TypeScript utilizado em todo o projeto
- Interfaces bem definidas
- Melhor DX e menos erros em produção 