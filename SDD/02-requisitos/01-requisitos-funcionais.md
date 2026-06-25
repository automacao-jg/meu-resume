# Requisitos Funcionais

## RF01 — Upload de currículo

- O usuário pode fazer upload de arquivo PDF (máx. 5MB)
- O usuário pode colar o texto do currículo diretamente
- O sistema extrai o texto do PDF automaticamente
- Validação: rejeitar arquivos que não sejam PDF ou que estejam em branco

## RF02 — Configuração da conversão

- O usuário informa a área de atuação / cargo desejado (campo livre)
- O usuário seleciona os idiomas de saída: inglês, francês ou ambos
- O usuário indica se deseja cover letter (sim/não)
- Opcional: campo para informar empresa-alvo (personaliza cover letter)

## RF03 — Geração via IA

- O sistema envia o currículo + configurações para a Claude API
- Claude gera o currículo canadense formatado em inglês
- Claude gera o currículo canadense formatado em francês (se solicitado)
- Claude gera a cover letter (se solicitada)
- Timeout máximo: 120 segundos

## RF04 — Download dos resultados

- O sistema gera arquivos `.docx` para cada saída
- O usuário pode baixar cada arquivo individualmente
- Os arquivos ficam disponíveis por 24h após a geração
- Nomenclatura: `meuresume_en.docx`, `meuresume_fr.docx`, `coverletter_en.docx`

## RF05 — Autenticação e conta

- Cadastro com e-mail + senha
- Login com Google (OAuth)
- Recuperação de senha por e-mail
- Perfil básico: nome, e-mail, país de destino no Canadá

## RF06 — Controle de uso (créditos)

- Cada conversão consome 1 crédito
- Plano Free: X créditos grátis para experimentar
- Plano Pago: créditos ilimitados ou pacote mensal
- Exibir saldo de créditos no dashboard
- Bloquear geração se saldo = 0 (com CTA para upgrade)

## RF07 — Histórico

- O usuário pode ver suas conversões anteriores
- Pode baixar novamente qualquer conversão dos últimos 30 dias

---

## Casos de uso resumidos

| ID | Ator | Ação |
|---|---|---|
| UC01 | Usuário | Faz upload do currículo e recebe versão canadense |
| UC02 | Usuário | Gera cover letter para vaga específica |
| UC03 | Usuário | Baixa arquivo `.docx` gerado |
| UC04 | Usuário | Assina plano para mais créditos |
| UC05 | Sistema | Envia currículo para Claude API e retorna resultado |
