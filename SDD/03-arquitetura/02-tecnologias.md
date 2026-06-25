# Tecnologias e Justificativas

## Stack principal

| Tecnologia | Versão alvo | Papel |
|---|---|---|
| Next.js | 14+ (App Router) | Framework full-stack |
| React | 18+ | UI |
| Tailwind CSS | 3+ | Estilização |
| TypeScript | 5+ | Tipagem estática |
| Supabase | — | BaaS (Auth + DB + Storage) |
| Claude API | claude-sonnet-4-6 | IA para geração de texto |
| Vercel | — | Deploy e hospedagem |
| Lovable | — | Geração de UI |

## Bibliotecas adicionais

| Biblioteca | Uso |
|---|---|
| `docx` (npm) | Geração de arquivos .docx |
| `pdf-parse` | Extração de texto de PDFs |
| `@supabase/supabase-js` | SDK do Supabase |
| `@anthropic-ai/sdk` | SDK da Claude API |
| `zod` | Validação de schemas |
| `stripe` | Pagamentos (pós-MVP) |

## Decisões técnicas

### Por que Next.js App Router e não Pages Router?
App Router é o padrão atual, suporta Server Components nativamente e tem melhor integração com Vercel.

### Por que Supabase e não Firebase?
Supabase é open source, usa PostgreSQL (SQL real), e tem Row Level Security nativo — essencial para proteger dados de currículo de diferentes usuários.

### Por que Claude e não GPT-4 ou Gemini?
Qualidade superior na geração de texto profissional e currículos. Jussara já tem conta na Anthropic API.

### Por que Lovable para UI?
Acelera a geração do frontend sem precisar de designer, permitindo foco na lógica de negócio e prompts.

### Por que docx (npm) para geração de arquivo?
Biblioteca matura, sem dependência de LibreOffice no servidor, funciona perfeitamente em ambiente serverless (Vercel Functions).
