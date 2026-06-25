# SDD — Meu Resumé
**Software Design Document v1.0**
_Última atualização: Junho 2026_

---

## Objetivo do documento

Este SDD descreve a arquitetura, requisitos e decisões técnicas do **Meu Resumé** (meuresume.com) — um SaaS que converte currículos no formato brasileiro para o padrão canadense (inglês e francês), com geração de cover letter.

---

## Escopo do sistema

- Upload de currículo brasileiro (PDF ou texto)
- Conversão para formato canadense via Claude API
- Geração em inglês e francês
- Geração de cover letter personalizada
- Download do resultado em `.docx`
- Autenticação de usuários e controle de uso (créditos/plano)

---

## Referências e stakeholders

| Papel | Nome |
|---|---|
| Fundadora / Dev | Jussara |
| Usuário-alvo | Brasileiros buscando emprego no Canadá |

---

## Como navegar no SDD

| Seção | O que você encontra |
|---|---|
| [01-visao-geral/](./01-visao-geral/01-contexto.md) | Contexto, motivação e objetivos |
| [02-requisitos/](./02-requisitos/01-requisitos-funcionais.md) | Requisitos funcionais e não funcionais |
| [03-arquitetura/](./03-arquitetura/01-visao-arquitetural.md) | Stack, camadas e diagramas |
| [04-design-detalhado/](./04-design-detalhado/01-modelo-dados.md) | Banco de dados, módulos e fluxos |
| [05-seguranca/](./05-seguranca/01-autenticacao-autorizacao.md) | Autenticação, LGPD, proteção de dados |
| [06-testes/](./06-testes/01-estrategia-testes.md) | Estratégia e casos de teste |
| [07-operacional/](./07-operacional/01-deploy.md) | Deploy, monitoramento e backup |
| [08-anexos/](./08-anexos/glossario.md) | Glossário e referências |
