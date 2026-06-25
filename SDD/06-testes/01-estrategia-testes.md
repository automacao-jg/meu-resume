# Estratégia de Testes

## Abordagem geral

Para o MVP, foco em testes manuais + smoke tests automatizados. Testes unitários completos são pós-MVP.

---

## Tipos de teste

### 1. Testes manuais (MVP)
Executar antes de cada deploy em produção.

**Checklist mínimo:**
- [ ] Upload de PDF real → conversão concluída com sucesso
- [ ] Download do .docx → arquivo abre no Word sem erros
- [ ] Login com e-mail funciona
- [ ] Login com Google funciona
- [ ] Usuário sem créditos vê mensagem de bloqueio
- [ ] Currículo em inglês está no formato canadense correto
- [ ] Currículo em francês está no formato canadense correto
- [ ] Cover letter referencia o cargo informado

### 2. Testes de integração (prioritários)

| Caso | Entrada | Esperado |
|---|---|---|
| PDF válido | CV em PT-BR | .docx gerado corretamente |
| PDF ilegível/corrompido | Arquivo inválido | Erro 400 com mensagem clara |
| PDF sem texto (só imagem) | Scan sem OCR | Erro explicativo ao usuário |
| Texto muito curto | < 100 caracteres | Validação rejeita antes de chamar Claude |
| Claude API timeout | Simular timeout | Retry + mensagem de erro ao usuário |
| Usuário sem créditos | 0 créditos | Bloqueio antes de chamar Claude |

### 3. Testes de qualidade do output (crítico)
Verificar manualmente com 3-5 currículos reais de teste:
- Summary tem máximo 4 linhas?
- Core Competencies está em tabela de 3 colunas?
- Datas no formato canadense (May 2023 – Present)?
- Nenhum dado pessoal brasileiro vazou (CPF, RG, data de nascimento, estado civil)?
- Linguagem está em inglês canadense (não britânico nem americano)?

---

## Critérios de aceitação para ir ao ar

- [ ] Conversão funciona para 5 currículos de teste diferentes
- [ ] Nenhum erro 500 nos últimos 10 testes manuais
- [ ] .docx abre corretamente no Word Online e Google Docs
- [ ] Login e cadastro funcionam end-to-end
- [ ] Débito de créditos funciona corretamente
