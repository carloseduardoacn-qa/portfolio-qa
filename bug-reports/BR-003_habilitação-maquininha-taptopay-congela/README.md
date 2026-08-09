BR-003 - App InterBusiness congela e impede avanço na habilitação do recurso Tap to Pay

## Informações Gerais

| Campo | Detalhe |
| :--- | :--- |
| **ID** | BR-003 |
| **Título** | App InterBusiness congela e impede avanço na habilitação do Tap to Pay |
| **Reportado por** | QA Tester (Portfólio) |
| **Data do Teste** | 09/08/2026 |
| **Severidade** | Alta |
| **Prioridade** | Alta |
| **Status** | Aberto |

---

## Justificativa de Severidade e Prioridade

* **Severidade (Alta):** Causa o congelamento da interface do usuário (*Unresponsive UI / UI Frozen*), bloqueando completamente a funcionalidade e exigindo o encerramento forçado do aplicativo.
* **Prioridade (Alta):** O recurso de maquininha (*Tap to Pay*) é uma funcionalidade crítica de transação e recebimento financeiro para contas PJ/Business.

---

## Ambiente de Teste

| Campo | Detalhe |
| :--- | :--- |
| **Aplicação** | InterBusiness |
| **Dispositivo** | *[Preencher modelo exato do dispositivo utilizado]* |
| **Sistema Operacional** | *[Preencher versão do SO, ex: iOS 18.x ou Android 14]* |
| **Versão do App** | *[Preencher versão exata do app InterBusiness]* |
| **Conexão** | Wi-Fi / Dados Móveis |

---

## Pré-condições

* Usuário autenticado em uma conta PJ/Business no aplicativo InterBusiness.
* Dispositivo com suporte à tecnologia NFC / Tap to Pay.

---

## Passos para Reprodução

1. Abrir o aplicativo **InterBusiness**.
2. Navegar até a funcionalidade de habilitação de maquininha (**Tap to Pay**).
3. Acionar a opção para habilitar a maquininha no dispositivo.

---

## Resultado Atual

O aplicativo congela (*Unresponsive UI / UI Frozen*) durante o processo de habilitação. A tela deixa de responder aos toques, o progresso da habilitação não avança e nenhuma mensagem de erro ou feedback visual é exibido, tornando necessário forçar o fechamento do app.

---

## Resultado Esperado

O aplicativo deve processar a solicitação de habilitação com sucesso ou, em caso de inconsistência de requisitos/comunicação, exibir uma mensagem clara e responsiva com tratamento de erro adequado, permitindo ao usuário cancelar ou tentar novamente sem a necessidade de fechar o app.

---

## Impacto

* Inviabiliza a ativação do *Tap to Pay*, impedindo o cliente de realizar vendas e transações no aplicativo.
* Compromete a usabilidade do aplicativo ao exigir que o usuário encerre forçadamente a aplicação.

---

## Evidências

* **Vídeo da Reprodução:** `Screencast01.mp4`
* **Captura de Tela:** `Screenshot01.jpeg`
* **Logs do Sistema:** `[Anexar arquivo .log do dispositivo ou console log se disponível]`
"""

filename = "BR-002-interbusiness-tap-to-pay.md"
with open(filename, "w", encoding="utf-8") as f:
    f.write(md_content)

print(f"File generated successfully: {filename}")
