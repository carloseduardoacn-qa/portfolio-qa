# BR-001 — Formulário de Contato: Loading Infinito e Ausência de Feedback ao Usuário

## Informações Gerais

| Campo | Detalhe |
|---|---|
| **ID** | BR-001 |
| **Título** | Formulário de contato não exibe feedback após envio — loading infinito |
| **Reportado por** | QA Tester (Portfólio) |
| **Data do Teste** | 13/05/2026 |
| **Severidade** | Alta |
| **Prioridade** | Alta |
| **Status** | Aberto |

---

## Ambiente de Teste

| Campo | Detalhe |
|---|---|
| **Site** | http://yuricogumelos.com.br |
| **Seção** | "Entre em Contato" |
| **Navegador** | Google Chrome 147.0.7727.138 (64 bits) |
| **Sistema Operacional** | Windows 11 Home Single Language — Versão 23H2 (Build 22631.6199) |
| **Servidor** | nginx/1.22.1 |
| **Tecnologia** | WordPress + Contact Form 7 v5.1.7 |
| **PHP** | 7.0.33 (desatualizado — EOL desde dezembro/2018) |

---

## Descrição

Ao preencher e enviar o formulário de contato da página principal, o botão **"ENVIAR"** exibe um ícone de carregamento (spinning) de forma indefinida, sem retornar nenhuma mensagem de sucesso ou erro ao usuário.

A requisição POST chega ao servidor e retorna um **erro HTTP 500 (Internal Server Error)**, porém essa falha não é comunicada visualmente ao usuário — a página permanece com o loading ativo indefinidamente.

---

## Passos para Reproduzir

1. Acessar http://yuricogumelos.com.br
2. Rolar a página até a seção **"Entre em Contato"**
3. Preencher os campos do formulário:
   - **Nome:** Teste QA Silva
   - **Telefone:** (11) 99999-9999
   - **E-mail:** teste.qa@email.com
   - **Assunto:** Teste de formulário
   - **Mensagem:** Mensagem de teste para validação do formulário.
4. Clicar no botão **"ENVIAR"**
5. Observar o comportamento da página após o clique

---

## Resultado Esperado

Exibição de mensagem de feedback ao usuário após o envio, como:
- ✅ `"Sua mensagem foi enviada com sucesso!"` — em caso de sucesso
- ❌ `"Ocorreu um erro ao enviar sua mensagem. Tente novamente."` — em caso de falha

---

## Resultado Obtido

O botão **"ENVIAR"** exibe um ícone de carregamento (loading) de forma indefinida. Nenhuma mensagem de retorno é exibida ao usuário. A página permanece no mesmo estado sem qualquer resposta visual, impossibilitando que o usuário saiba se sua mensagem foi ou não enviada.

---

## Análise Técnica

### Requisição com Falha

| Campo | Valor |
|---|---|
| **Endpoint** | `POST http://yuricogumelos.com.br/index.php/wp-json/contact-form-7/v1/contact-forms/6/feedback` |
| **Método** | POST |
| **Status Code** | `500 Internal Server Error` |
| **Tempo de Resposta** | 2682.3ms |
| **Tamanho** | 0.9 kB |

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

### Erros identificados no Console

```
POST http://yuricogumelos.com.br/index.php/wp-json/contact-form-7/v1/contact-forms/6/feedback
500 (Internal Server Error)
```

---

## Causa Raiz Provável

O erro 500 indica falha interna no servidor WordPress ao processar o envio do formulário. As causas mais prováveis são:

1. **Configuração de e-mail ausente ou incorreta no WordPress** — o servidor não consegue disparar o e-mail de confirmação
2. **Incompatibilidade entre Contact Form 7 v5.1.7 e PHP 7.0.33** — a versão do PHP está desatualizada (EOL desde dezembro/2018) e pode causar falhas de processamento
3. **Erro de plugin ou tema** conflitando com o Contact Form 7

---

## Impacto

- Usuário não tem como confirmar se sua mensagem foi enviada
- Pode gerar reenvios duplicados por falta de feedback
- Gera desconfiança na marca e no site
- Contatos comerciais potenciais são perdidos silenciosamente

---

## Observação de Segurança

> ⚠️ **PHP 7.0.33 desatualizado**
> O servidor está rodando PHP versão 7.0.33, que atingiu End of Life (EOL) em dezembro de 2018 e não recebe mais atualizações de segurança. Recomenda-se atualização para PHP 8.1 ou superior como medida de segurança independente deste bug.

---

## Evidências

| # | Tipo | Descrição |
|---|---|---|
| 01 | 📸 Screenshot | Formulário preenchido antes do envio |
| 02 | 📸 Screenshot | Loading infinito visível após clique em Enviar |
| 03 | 📸 Screenshot | Console com erro 500 destacado |
| 04 | 📸 Screenshot | Aba Network com requisição feedback em vermelho |
| 05 | 📸 Screenshot | Headers da requisição — URL, método POST, status 500 |
| 06 | 📸 Screenshot | Response da requisição — mensagem internal_server_error |
| 07 | 🎥 Vídeo | Reprodução completa do bug (Loom): https://www.loom.com/share/2eec57f1c8394f15b82d726757515230 |
| 08 | 📁 HAR File | `BR-001_formulario-contato-500.har` — captura completa da sessão de rede |

---

## Sugestão de Correção

1. Verificar e corrigir a configuração de envio de e-mail no WordPress (SMTP)
2. Atualizar o PHP para versão 8.1 ou superior
3. Atualizar o plugin Contact Form 7 para a versão mais recente
4. Implementar tratamento de erro no frontend para exibir mensagem ao usuário em caso de falha no envio

---

*Bug report gerado como parte de portfólio prático de QA — testes exploratórios em sites públicos.*
