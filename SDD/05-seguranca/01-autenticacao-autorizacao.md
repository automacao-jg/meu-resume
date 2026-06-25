# Segurança

## Autenticação e Autorização

### Supabase Auth
- JWT tokens com expiração de 1 hora
- Refresh tokens para sessão persistente
- Login via e-mail/senha e OAuth Google

### Proteção de rotas
- Todas as rotas `/dashboard`, `/convert`, `/result` exigem sessão ativa
- Middleware Next.js valida token JWT em cada requisição
- API Routes validam `user_id` da sessão antes de qualquer operação

### Row Level Security (RLS)
- Habilitado em todas as tabelas
- Políticas: usuário só acessa registros com `user_id = auth.uid()`
- Backend usa `service_role` key apenas em operações administrativas

---

## Proteção de dados (LGPD)

### Dados sensíveis tratados
- Currículo completo (dados pessoais, profissionais)
- E-mail e nome do usuário

### Medidas adotadas
- Currículos armazenados em bucket privado no Supabase Storage
- Arquivos gerados expiram em 30 dias
- Opção de exclusão de conta apaga todos os dados (LGPD Art. 18)
- Consentimento explícito no cadastro (checkbox + link para política)

### O que é enviado para Anthropic
- Texto do currículo é enviado para a Claude API para processamento
- Documentar na política de privacidade: "Seus dados são processados pela Anthropic para geração do conteúdo. Consulte a política de privacidade da Anthropic."

---

## Segurança de infraestrutura

| Medida | Implementação |
|---|---|
| HTTPS | Vercel (automático) |
| Variáveis secretas | Vercel Environment Variables (nunca no código) |
| API Key Claude | Apenas no servidor (nunca exposta ao cliente) |
| Supabase Keys | `anon key` no cliente, `service_role` apenas no servidor |
| Rate limiting | Vercel Edge + validação de créditos no backend |

---

## Controles e políticas

- **Sem acesso admin a dados de usuários** sem solicitação explícita
- **Logs de conversão** sem o conteúdo do currículo (só metadata)
- **Auditoria**: tabela `conversions` registra timestamp e user_id de toda ação
