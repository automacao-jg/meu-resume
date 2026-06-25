# Requisitos Não Funcionais

## RNF01 — Performance

- Tempo de resposta da geração: < 60s para currículo simples, < 120s para currículo + cover letter + 2 idiomas
- Carregamento de página: < 3s (LCP)
- Upload de PDF: processamento em < 5s

## RNF02 — Disponibilidade

- Uptime mínimo: 99% (Vercel SLA)
- Sem janela de manutenção programada no MVP
- Dependência crítica: Claude API (monitorar status em status.anthropic.com)

## RNF03 — Segurança

- HTTPS obrigatório em todos os endpoints
- Tokens JWT com expiração de 1h (Supabase Auth)
- Currículos armazenados criptografados no Supabase Storage
- Dados excluídos após 30 dias de inatividade do usuário
- Sem compartilhamento de dados com terceiros além de Anthropic (processamento)

## RNF04 — Escalabilidade

- Arquitetura serverless (Vercel Functions): escala automaticamente
- Supabase: plano Free aguenta MVP; upgrade para Pro conforme crescimento
- Claude API: pay-per-use, sem gargalo de infra

## RNF05 — Usabilidade

- Interface em português brasileiro
- Resultado da conversão entregue sem necessidade de instruções
- Feedback visual claro durante o processamento (loading state)
- Mensagens de erro em linguagem humana (não técnica)

## RNF06 — Conformidade

- LGPD: consentimento explícito para processamento de dados
- Política de privacidade clara antes do cadastro
- Direito de exclusão de conta e dados (LGPD Art. 18)

## RNF07 — Manutenibilidade

- Código versionado no GitHub
- Variáveis sensíveis apenas em `.env` (nunca commitadas)
- Logs estruturados para debug de erros de geração
