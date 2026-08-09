# BR-002 — Botão "Enter Password" não responde ao toque e não exibe feedback visual na Apple Wallet após Modo Perdido

## Informações Gerais

| Campo | Detalhe |
|---|---|
| ID | BR-002 |
| Título | Botão "Enter Password" não responde ao toque e não exibe feedback visual na Apple Wallet após Modo Perdido |
| Reportado por | QA Tester (Portfólio) |
| Data do Teste | 08/08/2026 |
| Severidade | Alta |
| Prioridade | Alta |
| Status | Aberto |

### Justificativa de Severidade

**Alta** — Impede que o usuário reative e utilize seus cartões de pagamento (Apple Pay) após recuperar o dispositivo do Modo Perdido. Trata-se de um bloqueio funcional direto em um recurso crítico do sistema operacional (UI congelada/unresponsive UI).

### Justificativa de Prioridade

**Alta** — O aplicativo Apple Wallet lida com pagamentos e transações financeiras do usuário. A impossibilidade de reautenticar a conta impede o uso do serviço de pagamento, impactando diretamente a experiência do usuário.

---

## Ambiente de Teste

| Campo | Detalhe |
|---|---|
| Aplicativo | Apple Wallet / iOS System UI |
| Dispositivo | iPhone |
| Sistema Operacional | iOS (Versão Atual) |
| Funcionalidade | Apple Account Verification / Recovery |

---

## Descrição

Ao tentar reativar os cartões na Apple Wallet após desativar o **Lost Mode** (Modo Perdido), a interface exibe a mensagem de alerta *"Apple Account Verification Required"*. 

No entanto, ao clicar no botão **"Enter Password"**, o aplicativo não responde ao comando (unresponsive UI), não abre a tela de autenticação da Apple Account e não exibe nenhuma mensagem de erro ou feedback ao usuário, travando o fluxo de recuperação do Apple Pay.

---

## Passos para Reproduzir

1. Marcar o dispositivo como perdido via Buscar (*Find My*) ativando o **Lost Mode**.
2. Desativar o **Lost Mode** através do painel de gerenciamento do iCloud.
3. Abrir o aplicativo **Apple Wallet** no dispositivo.
4. Selecionar um cartão suspenso (ex: PicPay Mastercard final 7039).
5. No banner de alerta *"Apple Account Verification Required"*, tocar no botão **"Enter Password"**.
6. Observar a falta de resposta da interface ao clique/toque.

---

## Resultado Esperado

Ao clicar no botão **"Enter Password"**, o sistema deve abrir a tela modal/prompt de autenticação do iOS solicitando a senha da Apple Account para revalidar os cartões e restabelecer o serviço do Apple Pay.

---

## Resultado Obtido

O botão **"Enter Password"** não responde ao toque. Nenhuma ação é executada, nenhuma tela modal é aberta e nenhum feedback visual/sonoro é apresentado ao usuário, mantendo os cartões travados no estado "Suspenso".

---

## Análise Técnica

### Comportamento Observado

- **Evento:** Clique/Toque no elemento interativo de CTA (*Call to Action*).
- **Falha de UI/UX:** O componente do botão não aciona a rota de navegação/módulo de autenticação nativo (`AuthenticationServices` / `LocalAuthentication`).
- **Estado do App:** O aplicativo permanece na mesma tela sem registrar a interação, sugerindo falha no *event handler* do botão ou bloqueio assíncrono na verificação de estado da conta.

---

## Análise Técnica / Hipóteses

 Com base no comportamento observado, o problema pode estar relacionado a:

1. **Falha de Binding de Evento de UI:** O evento de toque (`onTouch/onClick`) no botão "Enter Password" não está mapeado ou habilitado corretamente no estado do banner de verificação.
2. **Conflito de Estado de Sincronização:** Falha de comunicação entre o estado da conta sincronizado via iCloud (desativação do Lost Mode) e a verificação local de segurança do dispositivo.
3. **Bloqueio de Módulo de Autenticação Nativa:** O serviço responsável por invocar o prompt de credenciais falha silenciosamente sem capturar ou tratar a exceção (*unhandled exception*).

> **Nota de QA:** A confirmação da causa raiz exige análise dos logs do console do iOS (via Xcode / Sysdiagnose) durante a reprodução do evento.

---

## Impacto

- O usuário fica permanentemente impossibilitado de utilizar os cartões cadastrados no Apple Pay após o uso do Modo Perdido.
- A ausência de feedback passa a impressão de tela congelada ou travamento da aplicação.
- Quebra de confiança no recurso de segurança e recuperação do iOS/iCloud.

---

## Evidências

| # | Tipo | Descrição |
|---|---|---|
| 01 | 📸 Screenshot | [Exibição do banner de verificação do Apple Wallet](./01-apple-wallet-banner.png) |
| 02 | 🎥 Vídeo | [Demonstração do botão "Enter Password" sem resposta](./02-evidencia-toque-sem-resposta.mp4) |

> *(Ajuste os nomes dos arquivos de imagem/vídeo da tabela acima de acordo com os arquivos reais que você colocar na pasta).*

---

## Sugestão de Investigação / Correção

1. Capturar e analisar o *sysdiagnose* do iOS no momento da interação com o botão.
2. Validar se a chamada para a API de autenticação nativa está sendo invocada ao disparar o evento de clique.
3. Adicionar tratamento de exceções para garantir que, caso a autenticação falhe ao abrir, uma mensagem de erro compreensível seja exibida ao usuário.
4. Testar o fluxo de transição do estado "Lost Mode -> Normal Mode" na sincronização do iCloud.

---

## Classificação

**Tipo:** Functional Bug / UI Unresponsive  
**Área:** Mobile App / Security Authentication  
**Componente afetado:** Apple Wallet UI / iCloud Account Authentication / iOS UI Event Handling  
**Reprodutibilidade:** Reproduzido durante o teste  

---

> Bug report desenvolvido como parte de portfólio prático de QA, com base em testes exploratórios realizados em ambiente iOS.
