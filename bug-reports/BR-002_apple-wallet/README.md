# [BUG] Botão "Enter Password" não responde ao toque e não exibe feedback visual na Apple Wallet após Modo Perdido

## 1. Descrição do Problema
Ao tentar reativar os cartões na Apple Wallet após desativar o **Lost Mode** (Modo Perdido), a interface exibe a mensagem de alerta `"Apple Account Verification Required"`. No entanto, ao clicar no botão **"Enter Password"**, o aplicativo **não responde ao comando (unresponsive UI)**, não abre a tela de autenticação da Apple Account e **não exibe nenhuma mensagem de erro ou feedback ao usuário**, travando o fluxo de recuperação do Apple Pay.

---

## 2. Passos para Reprodução
1. Marque o dispositivo como perdido via Buscar (Find My) ativando o **Lost Mode**.
2. Desative o **Lost Mode** através do painel de gerenciamento do iCloud.
3. Abra o aplicativo **Apple Wallet** no dispositivo.
4. Selecione um cartão suspenso (ex: PicPay Mastercard final 7039).
5. No banner de alerta `"Apple Account Verification Required"`, toque no botão **"Enter Password"**.
6. Observe que o botão não executa nenhuma ação e o sistema permanece estático.

---

## 3. Comportamento Esperado
Ao tocar no botão **"Enter Password"**, o sistema operacional deveria abrir imediatamente a modal/prompt do sistema para digitação da senha da Apple Account (ou autenticação biométrica Face ID/Touch ID) para reativar os cartões. Caso ocorra uma falha de conexão ou autenticação, o aplicativo deveria exibir uma mensagem de erro clara.

---

## 4. Comportamento Atual
O botão **"Enter Password"** é completamente inativo ao toque (*unresponsive*). Nenhuma janela de autenticação é aberta, nenhum spinner de carregamento é exibido e nenhuma mensagem de erro ou feedback visual/sonoro é apresentado ao usuário, mantendo os cartões permanentemente bloqueados.

---

## 5. Severidade e Impacto
* **Severidade:** Alta / Crítica (Bloqueio de funcionalidade principal)
* **Impacto:** Impedimento total do uso do Apple Pay para pagamentos por aproximação (NFC) e gestão de carteira após recuperação de dispositivo perdido, sem alternativas para o usuário dentro do app.

---

## 6. Ambiente de Teste
* **Dispositivo:** iPhone
* **Sistema Operacional:** iOS (Preencher a versão exata, ex: iOS 17.5.1 / iOS 18.0)
* **App:** Apple Wallet / Apple Pay
* **Cartão Afetado:** PicPay Mastercard (final 7039) / Banco Inter (e outros cartões no stack)

---

## 7. Evidências Visuais
* **Captura de Tela:**
  ![Banner de Verificação sem resposta](https://github.com/user-attachments/assets/SEU_LINK_DA_IMAGEM_AQUI)

* **Gravação de Tela (Vídeo Demonstrativo):**
  [Assistir ao vídeo de reprodução do bug sem resposta do botão](https://github.com/user-attachments/assets/SEU_LINK_DO_VIDEO_AQUI)
