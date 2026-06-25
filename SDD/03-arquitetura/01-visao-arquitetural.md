# Visão Arquitetural

## Diagrama de camadas

```
┌─────────────────────────────────────────┐
│              FRONTEND                   │
│   Next.js (App Router) + Tailwind CSS   │
│   Gerado com Lovable                    │
└────────────────┬────────────────────────┘
                 │ API Routes (Next.js)
┌────────────────▼────────────────────────┐
│              BACKEND                    │
│   Next.js API Routes (serverless)       │
│   Lógica de negócio + orquestração      │
└──────┬──────────────┬───────────────────┘
       │              │
┌──────▼──────┐  ┌───▼──────────────────┐
│  Supabase   │  │    Claude API         │
│  - Auth     │  │  claude-sonnet-4-6   │
│  - Postgres │  │  Geração de texto     │
│  - Storage  │  └──────────────────────┘
└─────────────┘
       │
┌──────▼──────┐
│   Vercel    │
│   Deploy    │
│   CDN       │
└─────────────┘
```

## Fluxo principal (happy path)

```
Usuário → Upload PDF
       → API Route /api/convert
       → Extração de texto (pdf-parse)
       → Prompt montado + chamada Claude API
       → Claude retorna texto formatado
       → Geração do .docx (docx library)
       → Upload para Supabase Storage
       → URL de download retornada ao frontend
       → Usuário baixa o arquivo
```

## Componentes e responsabilidades

| Componente | Responsabilidade |
|---|---|
| `Next.js Frontend` | UI, roteamento, estados de loading/erro |
| `Next.js API Routes` | Orquestração, validação, chamadas externas |
| `Supabase Auth` | Login, sessão, tokens JWT |
| `Supabase Postgres` | Usuários, histórico de conversões, créditos |
| `Supabase Storage` | Arquivos .docx gerados, PDFs enviados |
| `Claude API` | Geração do currículo canadense e cover letter |
| `pdf-parse` | Extração de texto de PDFs no servidor |
| `docx` (npm) | Geração dos arquivos .docx com formatação |
| `Vercel` | Hospedagem, CDN, variáveis de ambiente |
