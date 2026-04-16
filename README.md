
# 🔐 NFC Vault

Gerenciador de senhas pessoal de alta segurança com criptografia **AES-256-GCM**, sincronização automática em nuvem via **Firebase** e desbloqueio físico por **tag NFC**.

Este projeto utiliza uma arquitetura *Zero-Knowledge*: as suas senhas são criptografadas e descriptografadas apenas no seu navegador. A sua chave mestre (NFC) nunca é enviada para o servidor.

---

## 🚀 Como funciona

```text
Tag NFC (Chave Física) ou Chave Manual (64 hex)
        ↓
Interface solicita o desbloqueio
        ↓
Dados criptografados baixados do Firebase
        ↓
Vault descriptografado localmente no navegador
        ↓
Gerenciamento de senhas (Sincronização em tempo real)
```

As senhas **nunca saem do seu dispositivo** em texto claro. Sem a chave de 64 caracteres hexadecimais, os dados no banco de dados são completamente ilegíveis.

---

## 🛠️ Primeira configuração

### Pré-requisitos

* **Android**: Chrome 89+ (para suporte à Web NFC).
* **PC/Outros**: Qualquer navegador moderno (utilizando a chave manual).
* **Hardware**: Uma **tag NFC** (NTAG213 ou similar).
* **App Auxiliar**: [NFC Tools](https://play.google.com/store/apps/details?id=com.wakdev.wdnfc) (apenas para a gravação inicial da tag).

### Opção A — Criar um Vault Novo

1.  **Gere a chave**: No app, clique em **"Gerar chave aleatória"**. Copie o código gerado.
2.  **Grave na Tag**: No app **NFC Tools**, vá em `Write` -> `Add a record` -> `Text`, cole a chave de 64 caracteres e grave na tag.
3.  **Ative o Vault**: Volte ao NFC Vault e clique em **"Já gravei na tag — Criar Vault"**. O sistema criará seu espaço seguro no Firebase.

> ⚠️ **AVISO CRÍTICO:** Salve uma cópia desta chave em um local seguro (papel ou outro cofre). Se você perder a tag NFC e não tiver a chave anotada, **não há como recuperar as senhas**.

### Opção B — Acessar Vault Existente (Nuvem)

Se você já configurou o vault e quer acessar de outro dispositivo:
1.  Selecione **"Acessar meu Vault"**.
2.  **Via Nuvem**: Cole sua chave de 64 caracteres e clique em **"Entrar com Chave"**. O app baixará e abrirá seus dados automaticamente.
3.  **Via Arquivo**: Se tiver um backup `.nfcv`, você pode carregá-lo e usar a chave para descriptografar.

---

## 📱 Uso Diário

* **Desbloqueio NFC**: No Android, basta clicar em **"Aproximar tag NFC"** e encostar sua tag no aparelho.
* **Sincronização**: Toda alteração é salva automaticamente na nuvem. Você não precisa se preocupar em "salvar" o arquivo o tempo todo.
* **Filtros por Usuário**: Organize suas senhas criando usuários (ex: Matheus, Trabalho, Família) e filtre-as facilmente pelas abas superiores.

---

## ☁️ Backup e Proteção de Dados

O sistema oferece três camadas de segurança para seus dados:

1.  **Nuvem (Firebase)**: Sincronização global automática e persistente.
2.  **Telegram**: Envio manual de cópia criptografada para o seu próprio bot (útil como backup secundário externo).
3.  **Arquivo Local (.nfcv)**: Você pode baixar uma cópia criptografada para guardar de forma offline (pen drives, etc).

---

## 🔒 Segurança e Privacidade

| Recurso | Tecnologia / Detalhe |
| :--- | :--- |
| **Algoritmo** | AES-256-GCM (Criptografia Autenticada) |
| **Arquitetura** | *Zero-Knowledge* (Privacidade absoluta) |
| **Identificador** | ID do Vault gerado via SHA-256 da chave |
| **Infraestrutura** | Firebase Realtime Database (Google Cloud) |
| **Backup Extra** | Telegram Bot API integration |

---

## 🌐 Hospedagem (GitHub Pages)

Você pode hospedar este gerenciador para uso pessoal no GitHub:
1.  Crie um repositório no seu GitHub.
2.  Suba o arquivo `index.html`.
3.  Ative o **GitHub Pages** em `Settings > Pages`.
4.  **Configuração de Segurança**: No painel do Google Cloud, restrinja sua API Key para aceitar apenas requisições vindas do domínio `https://seu-usuario.github.io/*`.

---

## 🛠️ Tecnologias Utilizadas

* **Web Crypto API**: Criptografia de nível militar nativa do navegador.
* **Web NFC**: Comunicação com hardware NFC via NDEF.
* **Firebase SDK**: Banco de dados NoSQL em tempo real.
* **PWA**: Pode ser instalado na tela inicial do celular como um aplicativo nativo.

---
```
