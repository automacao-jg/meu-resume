# Fluxos e Módulos Principais

## Módulo 1: Conversão (core)

**Arquivo:** `app/api/convert/route.ts`

**Responsabilidades:**
1. Receber o upload (PDF ou texto)
2. Extrair texto do PDF via `pdf-parse`
3. Validar conteúdo mínimo
4. Montar prompt para Claude
5. Chamar Claude API
6. Parsear resposta
7. Gerar .docx(s)
8. Salvar no Supabase Storage
9. Registrar conversão no banco
10. Retornar URLs de download

**Fluxo de erro:**
- PDF ilegível → erro 400 com mensagem clara
- Claude timeout → retry 1x, depois erro 503
- Geração de .docx falha → erro 500 + log

---

## Módulo 2: Prompt Engine

**Arquivo:** `lib/prompts/resume-converter.ts`

Responsável por montar o prompt dinâmico para Claude.

**Variáveis do prompt:**
- Texto do currículo original
- Cargo desejado
- Idioma de saída (en/fr)
- Empresa-alvo (opcional, para cover letter)
- Instruções de formato canadense

**Estrutura do prompt:**
```
[SYSTEM] Você é um especialista em currículos canadenses...
[INSTRUÇÕES DE FORMATO]
[CURRÍCULO ORIGINAL]
[CARGO DESEJADO]
[OUTPUT ESPERADO em XML/JSON estruturado]
```

> ⚠️ O output da Claude deve ser estruturado (JSON) para facilitar a geração do .docx. Nunca retornar texto puro não estruturado.

---

## Módulo 3: Gerador de .docx

**Arquivo:** `lib/docx/resume-generator.ts`

Usa a biblioteca `docx` (npm) para gerar o arquivo Word.

**Seções do currículo canadense:**
1. Nome + Contato
2. Professional Summary (máx. 4 linhas)
3. Core Competencies (tabela 3 colunas)
4. Professional Experience (cronológica reversa)
5. Education
6. Certifications (se houver)

**Regras de formatação:**
- Fonte: Calibri 11pt
- Cor: apenas preto (#000000)
- Sem bordas visíveis exceto onde necessário
- Margens: 1 inch (US Letter)

---

## Módulo 4: Créditos

**Arquivo:** `lib/credits.ts`

- `checkCredits(userId)` → verifica saldo
- `deductCredits(userId, amount)` → debita após conversão bem-sucedida
- Transação atômica: só debita se conversão completou com sucesso

---

## Páginas principais (Next.js)

| Rota | Página |
|---|---|
| `/` | Landing page |
| `/auth/login` | Login / Cadastro |
| `/dashboard` | Dashboard do usuário + histórico |
| `/convert` | Página de conversão (upload + configuração) |
| `/result/[id]` | Página de resultado + downloads |
| `/pricing` | Planos e preços |
