# Casos de Teste — Formulário de Contato

## Informações Gerais

| Campo | Detalhe |
|---|---|
| **Site** | http://yuricogumelos.com.br |
| **Componente** | Formulário de Contato — Seção "Entre em Contato" |
| **Elaborado por** | QA Tester (Portfólio) |
| **Data de Criação** | 13/05/2026 |
| **Versão** | 1.0 |
| **Total de Casos** | 12 |

---

## Campos do Formulário

| Campo | Obrigatório |
|---|---|
| Seu Nome | ✅ Sim |
| Seu Telefone | ✅ Sim |
| Seu E-Mail | ✅ Sim |
| Assunto | ❌ Não |
| Mensagem | ❌ Não |

---

## Pré-condições Gerais

> Aplicáveis a todos os casos de teste abaixo:
> - Ter acesso à internet
> - Acessar http://yuricogumelos.com.br
> - Rolar a página até a seção "Entre em Contato"
> - Utilizar dados fictícios — nunca dados pessoais reais
> - Navegador: Google Chrome (versão atualizada)

---

## Suíte 1 — Caminho Feliz (Happy Path)

### CT-001 — Envio do formulário com todos os campos preenchidos e válidos

| Campo | Detalhe |
|---|---|
| **ID** | CT-001 |
| **Tipo** | Happy Path |
| **Prioridade** | Alta |

**Passos:**

| # | Ação | Dado de Teste |
|---|---|---|
| 1 | Acessar o site | http://yuricogumelos.com.br |
| 2 | Rolar até "Entre em Contato" | — |
| 3 | Preencher o campo Nome | `Teste QA Silva` |
| 4 | Preencher o campo Telefone | `(11) 99999-9999` |
| 5 | Preencher o campo E-Mail | `teste.qa@email.com` |
| 6 | Preencher o campo Assunto | `Teste de formulário` |
| 7 | Preencher o campo Mensagem | `Mensagem de teste para validação do formulário.` |
| 8 | Clicar em **ENVIAR** | — |

**Resultado Esperado:** Mensagem de confirmação exibida — ex: `"Sua mensagem foi enviada com sucesso!"`

**Resultado Obtido:** Loading infinito — sem feedback ao usuário

**Status:** ❌ Falhou

**Referência:** BR-001

---

### CT-002 — Envio do formulário sem o campo Assunto (opcional)

| Campo | Detalhe |
|---|---|
| **ID** | CT-002 |
| **Tipo** | Happy Path |
| **Prioridade** | Média |

**Passos:**

| # | Ação | Dado de Teste |
|---|---|---|
| 1 | Preencher o campo Nome | `Teste QA Silva` |
| 2 | Preencher o campo Telefone | `(11) 99999-9999` |
| 3 | Preencher o campo E-Mail | `teste.qa@email.com` |
| 4 | Deixar o campo Assunto **vazio** | — |
| 5 | Preencher o campo Mensagem | `Mensagem de teste.` |
| 6 | Clicar em **ENVIAR** | — |

**Resultado Esperado:** Formulário enviado com sucesso — campo opcional não deve bloquear o envio

**Resultado Obtido:** A verificar após correção do bug BR-001

**Status:** ⚠️ Bloqueado

---

### CT-003 — Envio do formulário sem o campo Mensagem (opcional)

| Campo | Detalhe |
|---|---|
| **ID** | CT-003 |
| **Tipo** | Happy Path |
| **Prioridade** | Média |

**Passos:**

| # | Ação | Dado de Teste |
|---|---|---|
| 1 | Preencher o campo Nome | `Teste QA Silva` |
| 2 | Preencher o campo Telefone | `(11) 99999-9999` |
| 3 | Preencher o campo E-Mail | `teste.qa@email.com` |
| 4 | Preencher o campo Assunto | `Teste de formulário` |
| 5 | Deixar o campo Mensagem **vazio** | — |
| 6 | Clicar em **ENVIAR** | — |

**Resultado Esperado:** Formulário enviado com sucesso — campo opcional não deve bloquear o envio

**Resultado Obtido:** A verificar após correção do bug BR-001

**Status:** ⚠️ Bloqueado

---

## Suíte 2 — Campos Obrigatórios (Negative Testing)

### CT-004 — Envio sem preencher o campo Nome

| Campo | Detalhe |
|---|---|
| **ID** | CT-004 |
| **Tipo** | Negativo |
| **Prioridade** | Alta |

**Passos:**

| # | Ação | Dado de Teste |
|---|---|---|
| 1 | Deixar o campo Nome **vazio** | — |
| 2 | Preencher o campo Telefone | `(11) 99999-9999` |
| 3 | Preencher o campo E-Mail | `teste.qa@email.com` |
| 4 | Clicar em **ENVIAR** | — |

**Resultado Esperado:** Mensagem de validação — ex: `"O campo Nome é obrigatório"`

**Resultado Obtido:** Sistema bloqueou o envio e exibiu duas mensagens:
mensagem específica abaixo do campo Nome ("The field is required.")
e mensagem geral abaixo do botão Enviar ("One or more fields have
an error. Please check and try again."). Ambas as mensagens estão
em inglês, em um site totalmente em português.

**Status:** ✅ Passou (com observação)

---

### CT-005 — Envio sem preencher o campo Telefone

| Campo | Detalhe |
|---|---|
| **ID** | CT-005 |
| **Tipo** | Negativo |
| **Prioridade** | Alta |

**Passos:**

| # | Ação | Dado de Teste |
|---|---|---|
| 1 | Preencher o campo Nome | `Teste QA Silva` |
| 2 | Deixar o campo Telefone **vazio** | — |
| 3 | Preencher o campo E-Mail | `teste.qa@email.com` |
| 4 | Clicar em **ENVIAR** | — |

**Resultado Esperado:** Mensagem de validação — ex: `"O campo Telefone é obrigatório"`

**Resultado Obtido:** A verificar

**Status:** 🔲 Não executado

---

### CT-006 — Envio sem preencher o campo E-Mail

| Campo | Detalhe |
|---|---|
| **ID** | CT-006 |
| **Tipo** | Negativo |
| **Prioridade** | Alta |

**Passos:**

| # | Ação | Dado de Teste |
|---|---|---|
| 1 | Preencher o campo Nome | `Teste QA Silva` |
| 2 | Preencher o campo Telefone | `(11) 99999-9999` |
| 3 | Deixar o campo E-Mail **vazio** | — |
| 4 | Clicar em **ENVIAR** | — |

**Resultado Esperado:** Mensagem de validação — ex: `"O campo E-Mail é obrigatório"`

**Resultado Obtido:** A verificar

**Status:** 🔲 Não executado

---

### CT-007 — Envio com E-Mail em formato inválido

| Campo | Detalhe |
|---|---|
| **ID** | CT-007 |
| **Tipo** | Negativo |
| **Prioridade** | Alta |

**Passos:**

| # | Ação | Dado de Teste |
|---|---|---|
| 1 | Preencher o campo Nome | `Teste QA Silva` |
| 2 | Preencher o campo Telefone | `(11) 99999-9999` |
| 3 | Preencher o campo E-Mail com formato inválido | `teste.qa` |
| 4 | Clicar em **ENVIAR** | — |

**Resultado Esperado:** Mensagem de validação — ex: `"Informe um e-mail válido"`

**Resultado Obtido:** A verificar

**Status:** 🔲 Não executado

---

### CT-008 — Envio com todos os campos obrigatórios vazios

| Campo | Detalhe |
|---|---|
| **ID** | CT-008 |
| **Tipo** | Negativo |
| **Prioridade** | Alta |

**Passos:**

| # | Ação | Dado de Teste |
|---|---|---|
| 1 | Deixar **todos** os campos vazios | — |
| 2 | Clicar em **ENVIAR** | — |

**Resultado Esperado:** Mensagens de validação em todos os campos obrigatórios

**Resultado Obtido:** A verificar

**Status:** 🔲 Não executado

---

## Suíte 3 — Casos de Borda (Edge Cases)

### CT-009 — Envio com Nome contendo apenas espaços em branco

| Campo | Detalhe |
|---|---|
| **ID** | CT-009 |
| **Tipo** | Edge Case |
| **Prioridade** | Média |

**Passos:**

| # | Ação | Dado de Teste |
|---|---|---|
| 1 | Preencher o campo Nome com espaços | `     ` |
| 2 | Preencher os demais campos com dados válidos | — |
| 3 | Clicar em **ENVIAR** | — |

**Resultado Esperado:** Validação deve rejeitar espaços em branco como nome válido

**Resultado Obtido:** A verificar

**Status:** 🔲 Não executado

---

### CT-010 — Envio com Telefone contendo letras

| Campo | Detalhe |
|---|---|
| **ID** | CT-010 |
| **Tipo** | Edge Case |
| **Prioridade** | Média |

**Passos:**

| # | Ação | Dado de Teste |
|---|---|---|
| 1 | Preencher o campo Nome | `Teste QA Silva` |
| 2 | Preencher o campo Telefone com letras | `abcde-fghij` |
| 3 | Preencher o campo E-Mail | `teste.qa@email.com` |
| 4 | Clicar em **ENVIAR** | — |

**Resultado Esperado:** Validação deve rejeitar letras no campo Telefone

**Resultado Obtido:** A verificar

**Status:** 🔲 Não executado

---

### CT-011 — Envio com caracteres especiais nos campos de texto

| Campo | Detalhe |
|---|---|
| **ID** | CT-011 |
| **Tipo** | Edge Case |
| **Prioridade** | Média |

**Passos:**

| # | Ação | Dado de Teste |
|---|---|---|
| 1 | Preencher o campo Nome com caracteres especiais | `<script>alert('teste')</script>` |
| 2 | Preencher os demais campos com dados válidos | — |
| 3 | Clicar em **ENVIAR** | — |

**Resultado Esperado:** Sistema deve tratar os caracteres especiais sem executar scripts ou quebrar o layout

**Resultado Obtido:** A verificar

**Status:** 🔲 Não executado

> 💡 Esse teste verifica vulnerabilidade de XSS (Cross-Site Scripting) — importante do ponto de vista de segurança.

---

### CT-012 — Envio com campo Mensagem no limite máximo de caracteres

| Campo | Detalhe |
|---|---|
| **ID** | CT-012 |
| **Tipo** | Edge Case |
| **Prioridade** | Baixa |

**Passos:**

| # | Ação | Dado de Teste |
|---|---|---|
| 1 | Preencher os campos obrigatórios com dados válidos | — |
| 2 | Preencher o campo Mensagem com 1000 caracteres | `AAAA...` (repetido até 1000 caracteres) |
| 3 | Clicar em **ENVIAR** | — |

**Resultado Esperado:** Sistema deve aceitar ou indicar claramente o limite máximo de caracteres

**Resultado Obtido:** A verificar

**Status:** 🔲 Não executado

---

## Resumo da Execução

| Status | Quantidade |
|---|---|
| ✅ Passou | 0 |
| ❌ Falhou | 1 |
| ⚠️ Bloqueado | 2 |
| 🔲 Não executado | 9 |
| **Total** | **12** |

> ⚠️ Os casos CT-002 ao CT-012 estão bloqueados ou pendentes de execução devido ao bug BR-001, que impede o funcionamento correto do formulário. Recomenda-se re-executar toda a suíte após a correção do bug.

---

*Casos de teste gerados como parte de portfólio prático de QA — testes sobre sites públicos.*
