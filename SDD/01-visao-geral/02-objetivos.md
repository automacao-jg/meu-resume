# Objetivos do Sistema

## Objetivos principais

1. **Conversão automática** de currículo BR → CA em < 60 segundos
2. **Saída em dois idiomas**: inglês canadense e francês canadense
3. **Cover letter** gerada junto com o currículo
4. **Download em .docx** com formatação profissional pronta para uso
5. **Self-service**: usuário faz tudo sem precisar de ajuda humana

## Requisitos de alto nível

- Interface simples: upload → aguardar → download
- Funcionar em desktop e mobile
- Suporte a PDF e texto copiado como entrada
- Resultado de qualidade profissional (não genérico)

## Restrições e premissas

| Restrição | Detalhe |
|---|---|
| Orçamento inicial | Bootstrap / sem investimento externo |
| Stack definida | Next.js + Supabase + Claude API + Vercel |
| Dev solo | Jussara (fundadora), com apoio de Lovable para frontend |
| MVP first | Começar com funcionalidade core antes de features extras |
| LGPD | Dados de currículo são sensíveis — tratamento adequado obrigatório |

## Justificativas de decisão

- **Next.js**: Full-stack em um só repositório, suporte a API routes, SSR
- **Supabase**: Auth + banco + storage prontos, sem gerenciar infra
- **Claude API**: Melhor qualidade de geração de texto profissional
- **Vercel**: Deploy simples, integração nativa com Next.js
- **Lovable**: Acelera geração de UI sem precisar de designer
