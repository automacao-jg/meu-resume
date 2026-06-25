# Deploy e Operação

## Ambientes

| Ambiente | URL | Branch |
|---|---|---|
| Desenvolvimento | localhost:3000 | qualquer |
| Preview | *.vercel.app | pull requests |
| Produção | meuresume.com | main |

---

## Deploy

### Processo
1. Push para branch `main` → deploy automático na Vercel
2. Vercel executa `next build`
3. Variáveis de ambiente configuradas no painel Vercel (não no código)
4. Deploy zero-downtime (Vercel padrão)

### Variáveis de ambiente necessárias
```
NEXT_PUBLIC_SUPABASE_URL=
NEXT_PUBLIC_SUPABASE_ANON_KEY=
SUPABASE_SERVICE_ROLE_KEY=
ANTHROPIC_API_KEY=
NEXT_PUBLIC_APP_URL=
```

> ⚠️ Nunca commitar variáveis reais. Usar `.env.local` localmente.

---

## Monitoramento e alertas

| O que monitorar | Como |
|---|---|
| Uptime da aplicação | Vercel Analytics (grátis) |
| Erros de runtime | Vercel Logs |
| Status Claude API | https://status.anthropic.com |
| Status Supabase | https://status.supabase.com |
| Uso de créditos de API | Painel Anthropic Console |

### Alertas manuais (MVP)
- Verificar logs Vercel 1x por dia nos primeiros 30 dias
- Configurar alerta de e-mail se uso da API Claude ultrapassar $X/dia

---

## Backup e recuperação

| Dado | Backup |
|---|---|
| Banco de dados | Supabase faz backup automático diário (plano Free: 1 dia, Pro: 7 dias) |
| Arquivos .docx | Supabase Storage (replicado internamente) |
| Código | GitHub (source of truth) |

### Recuperação de desastre
- Banco: restaurar via painel Supabase (point-in-time no plano Pro)
- Código: re-deploy a partir do GitHub
- Tempo estimado de recuperação: < 30 minutos

---

## Observabilidade

- Toda conversão é registrada na tabela `conversions` com status e timestamp
- Erros de Claude API logados no servidor com tipo de erro (sem conteúdo do currículo)
- Monitorar taxa de erro: se > 5% das conversões falharem em 1h → investigar imediatamente
