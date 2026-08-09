# BR-001 — Formulário de Contato permanece em loading infinito após erro HTTP 500

## Informações Gerais

| Campo | Detalhe |
|---|---|
| ID | BR-001 |
| Título | Formulário de contato permanece em loading infinito após erro HTTP 500 |
| Reportado por | QA Tester (Portfólio) |
| Data do Teste | 13/05/2026 |
| Severidade | Alta |
| Prioridade | Alta |
| Status | Aberto |

### Justificativa de Severidade

**Alta** — O fluxo de envio do formulário não é concluído corretamente e o usuário não recebe feedback sobre o resultado da operação. A requisição retorna HTTP 500 e a interface permanece em loading indefinidamente.

### Justificativa de Prioridade

**Alta** — O formulário representa um canal de contato comercial. A falha pode impedir ou dificultar o recebimento de potenciais contatos.

---

## Ambiente de Teste

| Campo | Detalhe |
|---|---|
| Site | http://yuricogumelos.com.br |
| Seção | "Entre em Contato" |
| Navegador | Google Chrome 147.0.7727.138 (64 bits) |
| Sistema Operacional | Windows 11 Home Single Language — Versão 23H2 (Build 22631.6199) |
| Servidor | nginx/1.22.1 |
| Tecnologia | WordPress + Contact Form 7 v5.1.7 |
| PHP | 7.0.33 (EOL) |

---

## Descrição

Ao preencher e enviar o formulário de contato da página principal, o botão **"ENVIAR"** exibe um ícone de carregamento (loading) de forma indefinida, sem retornar nenhuma mensagem de sucesso ou erro ao usuário.

Durante a investigação com as ferramentas de desenvolvedor, foi observado que a requisição `POST` responsável pelo envio chega ao servidor e retorna **HTTP 500 (Internal Server Error)**. Entretanto, essa falha não é comunicada visualmente ao usuário e a página permanece com o loading ativo indefinidamente.

---

## Passos para Reproduzir

1. Acessar http://yuricogumelos.com.br
2. Rolar a página até a seção **"Entre em Contato"**.
3. Preencher os campos do formulário:
   - **Nome:** Teste QA Silva
   - **Telefone:** (11) 99999-9999
   - **E-mail:** teste.qa@email.com
   - **Assunto:** Teste de formulário
   - **Mensagem:** Mensagem de teste para validação do formulário.
4. Clicar no botão **"ENVIAR"**.
5. Observar o comportamento da página após o clique.

---

## Resultado Esperado

Após o envio, o sistema deve apresentar feedback claro ao usuário informando o resultado da operação.

Exemplos:

- **Sucesso:** `"Sua mensagem foi enviada com sucesso!"`
- **Falha:** `"Ocorreu um erro ao enviar sua mensagem. Tente novamente."`

Em caso de falha no processamento, o usuário não deve permanecer indefinidamente em um estado de loading sem indicação do problema.

---

## Resultado Obtido

O botão **"ENVIAR"** exibe um ícone de carregamento de forma indefinida.

Nenhuma mensagem de sucesso ou erro é apresentada ao usuário. A página permanece no mesmo estado sem qualquer feedback visual, impossibilitando que o usuário saiba se sua mensagem foi ou não processada.

---

## Análise Técnica

### Requisição com Falha

| Campo | Valor |
|---|---|
| Endpoint | `POST http://yuricogumelos.com.br/index.php/wp-json/contact-form-7/v1/contact-forms/6/feedback` |
| Método | POST |
| Status Code | `500 Internal Server Error` |
| Tempo de Resposta | 2682.3ms |
| Tamanho | 0.9 kB |

### Response do Servidor

```json
{
  "code": "internal_server_error",
  "message": "Há um erro crítico no seu site.",
  "data": {
    "status": 500
  },
  "additional_errors": []
}
```

### Erro identificado no Console

```text
POST http://yuricogumelos.com.br/index.php/wp-json/contact-form-7/v1/contact-forms/6/feedback
500 (Internal Server Error)
```

### Interpretação

A evidência coletada confirma que o frontend recebe uma resposta **HTTP 500** ao tentar processar o envio do formulário.

O comportamento observado no frontend — loading infinito sem feedback — é uma consequência funcional relevante dessa falha, pois a interface não apresenta um estado de erro adequado ao usuário.

---

## Análise Técnica / Hipóteses

Com base nas evidências coletadas, é possível afirmar que existe uma falha interna no processamento da requisição no servidor.

Não foi possível determinar a causa raiz definitiva apenas pelos testes realizados. Algumas hipóteses que podem ser investigadas pela equipe responsável incluem:

1. Configuração de envio de e-mail ausente ou incorreta no WordPress.
2. Incompatibilidade entre componentes do ambiente, incluindo a versão do PHP e o Contact Form 7.
3. Erro ou conflito envolvendo plugin, tema ou configuração do WordPress.

> **Nota de QA:** As hipóteses acima não devem ser tratadas como causa raiz confirmada. A confirmação exigiria acesso aos logs do servidor e/ou investigação do ambiente backend.

---

## Impacto

- O usuário não consegue confirmar se sua mensagem foi enviada.
- A ausência de feedback pode levar o usuário a tentar reenviar a mensagem.
- Reenvios podem resultar em contatos duplicados.
- A falha pode gerar desconfiança na marca e no site.
- Contatos comerciais potenciais podem ser perdidos.

---

## Observação de Segurança

> ⚠️ **PHP 7.0.33 — versão EOL**
>
> O servidor observado utiliza PHP 7.0.33, uma versão que está fora de suporte. Essa informação é relevante para investigação e manutenção do ambiente, mas **não foi possível confirmar que a versão do PHP seja a causa do bug reportado**.

---

## Evidências

| # | Tipo | Descrição |
|---|---|---|
| 01 | 📸 Screenshot | Formulário preenchido antes do envio (https://github.com/carloseduardoacn-qa/portfolio-qa/blob/main/bug-reports/BR-001_formulario-contato-loading-infinito/01-formulario-preenchido.png)|
| 02 | 📸 Screenshot | Loading infinito visível após clique em Enviar https://github.com/carloseduardoacn-qa/portfolio-qa/blob/main/bug-reports/BR-001_formulario-contato-loading-infinito/02-loading-infinito.png|
| 03 | 📸 Screenshot | Console com erro 500 destacado |
| 04 | 📸 Screenshot | Aba Network com requisição de feedback em vermelho |
| 05 | 📸 Screenshot | Headers da requisição — URL, método POST e status 500 |
| 06 | 📸 Screenshot | Response da requisição — mensagem `internal_server_error` |
| 07 | 🎥 Vídeo | [Reprodução completa do bug (Loom)] (https://www.loom.com/share/2eec57f1c8394f15b82d726757515230) |
| 08 | 📁 HAR File | `BR-001_formulario-contato-500.har` — captura da sessão de rede |

---

## Sugestão de Investigação / Correção

1. Investigar os logs do servidor para identificar a origem do HTTP 500.
2. Verificar a configuração de envio de e-mail do WordPress e do Contact Form 7.
3. Verificar compatibilidade entre PHP, WordPress, Contact Form 7, plugins e tema utilizados.
4. Avaliar a atualização do PHP e dos componentes do WordPress para versões suportadas.
5. Implementar tratamento adequado de erro no frontend para impedir loading infinito e apresentar feedback ao usuário quando o envio falhar.

---

## Classificação

**Tipo:** Functional Bug / Backend + Frontend Behavior  
**Área:** Contact Form / Form Submission  
**Componente afetado:** Contact Form 7 / WordPress REST API / Frontend Feedback  
**Reprodutibilidade:** Reproduzido durante o teste

---

> Bug report desenvolvido como parte de portfólio prático de QA, com base em testes exploratórios realizados em site público.
