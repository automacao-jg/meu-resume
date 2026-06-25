# Modelo de Dados

## Tabelas Supabase (PostgreSQL)

### `users` (gerenciada pelo Supabase Auth)
Campos padrão do Supabase: `id`, `email`, `created_at`, etc.

---

### `profiles`
Extensão do usuário com dados da aplicação.

| Campo | Tipo | Descrição |
|---|---|---|
| `id` | uuid (FK → auth.users) | PK |
| `nome` | text | Nome completo |
| `provincia_destino` | text | Ex: Ontario, Quebec |
| `creditos` | integer | Saldo de créditos |
| `plano` | text | 'free' / 'pro' |
| `created_at` | timestamp | Data de cadastro |
| `updated_at` | timestamp | Última atualização |

---

### `conversions`
Histórico de cada conversão realizada.

| Campo | Tipo | Descrição |
|---|---|---|
| `id` | uuid | PK |
| `user_id` | uuid (FK → profiles) | Dono da conversão |
| `status` | text | 'processing' / 'done' / 'error' |
| `idiomas` | text[] | ['en', 'fr'] |
| `cover_letter` | boolean | Se gerou cover letter |
| `cargo_desejado` | text | Cargo/área informado |
| `empresa_alvo` | text | Empresa (opcional) |
| `input_storage_path` | text | Caminho do PDF no Storage |
| `output_en_path` | text | Caminho do .docx EN |
| `output_fr_path` | text | Caminho do .docx FR |
| `output_cl_path` | text | Caminho do .docx cover letter |
| `creditos_usados` | integer | Créditos consumidos |
| `created_at` | timestamp | Data da conversão |
| `expires_at` | timestamp | Quando os arquivos expiram |

---

## Storage (Supabase Storage)

### Bucket: `curriculos`
- Acesso: privado (só o dono)
- Estrutura: `{user_id}/{conversion_id}/input.pdf`

### Bucket: `outputs`
- Acesso: privado (só o dono)
- Estrutura: `{user_id}/{conversion_id}/meuresume_en.docx`
- Expiração: 30 dias

---

## Row Level Security (RLS)

Todas as tabelas habilitam RLS:
- Usuário só lê/escreve seus próprios dados
- Service Role (backend) tem acesso total
- Nenhum dado de currículo é público
