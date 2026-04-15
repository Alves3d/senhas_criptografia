# 🔐 NFC Vault

Gerenciador de senhas pessoal com criptografia **AES-256-GCM** e desbloqueio via **tag NFC**.  
Funciona 100% no navegador — sem servidor, sem conta, sem dependências externas.

---

## Como funciona

```
Tag NFC (chave física)
       ↓
Chrome Android lê a tag
       ↓
Vault descriptografado localmente
       ↓
Você vê e gerencia as senhas
       ↓
Fecha o Chrome → vault bloqueia automaticamente
```

As senhas **nunca saem do seu dispositivo** em texto claro. Sem a tag NFC, o arquivo de backup é ilegível.

---

## Primeira configuração

### Pré-requisitos

- **Android**: Chrome 89 ou superior (Web NFC nativo)
- **PC**: qualquer navegador moderno (desbloqueio manual pela chave)
- App **NFC Tools** instalado no Android ([Play Store](https://play.google.com/store/apps/details?id=com.wakdev.wdnfc))
- Uma **tag NFC** (NTAG213 ou similar — encontrada em papelaria ou lojas online)

### Passo a passo

**1. Abra o app**

Acesse `index.html` pelo Chrome. Na primeira vez, você verá a tela de configuração.

**2. Gere a chave de segurança**

Clique em **"Gerar chave aleatória"**.  
Uma chave de 64 caracteres hexadecimais será exibida.

> ⚠️ **Guarde essa chave em lugar seguro!** Se perder a tag NFC e não tiver a chave, não será possível recuperar as senhas.

**3. Grave a chave na tag NFC**

Abra o **NFC Tools** no Android:
1. Aba **Write**
2. **Add a record**
3. **Text**
4. Cole a chave de 64 caracteres
5. Toque em **Write** e aproxime a tag NFC do celular

**4. Crie o vault**

Volte ao NFC Vault e clique em **"Já gravei na tag — Criar Vault"**.  
Pronto! O vault está criado e você já está dentro.

---

## Uso diário

### Desbloquear (Android)

1. Abra o `index.html` no Chrome
2. Clique em **"Aproximar tag NFC"**
3. Encoste a tag no celular
4. Vault desbloqueado ✓

### Desbloquear (PC / Windows)

1. Abra o `index.html` no Chrome
2. Cole a chave de 64 caracteres no campo de texto
3. Clique em **"Desbloquear com chave"**

### Adicionar senha

> ⚠️ Cadastre pelo menos um usuário antes de adicionar senhas (veja seção abaixo).

1. Toque no botão **+** (canto inferior direito)
2. Preencha: nome do serviço, usuário/e-mail, senha, URL e selecione o dono
3. Use o botão 🎲 para gerar uma senha segura automaticamente
4. Clique em **"Adicionar senha"**

### Gerenciar usuários

Os usuários são as pessoas que vão usar o vault. Cada senha é vinculada a um usuário, permitindo filtrar por pessoa.

1. Na tela principal, toque no botão **👥** (canto superior esquerdo)
2. Digite o nome e clique em **"+ Adicionar usuário"**
3. Repita para cada pessoa (ex: Matheus, Pai, Mãe, etc.)
4. Para editar ou remover, use os ícones ✏️ e 🗑️ ao lado de cada usuário

### Outras ações

| Ação | Como fazer |
|---|---|
| Ver senha | Toque no ícone 👁️ na listagem |
| Copiar senha | Toque no ícone 📋 |
| Editar senha | Toque no card da senha |
| Excluir senha | Ícone 🗑️ no card ou dentro da edição |
| Filtrar por usuário | Abas no topo: Todos / nome de cada usuário |
| Gerenciar usuários | Botão 👥 no canto superior esquerdo |
| Bloquear | Botão 🔒 no canto superior direito |

---

## Backup e sincronização

> ⚠️ As senhas ficam no **localStorage do Chrome** — se limpar os dados do navegador ou trocar de dispositivo, o vault some. **Faça backup regularmente.**

### Exportar vault

1. Botão ⬇️ (canto superior direito) → **"Baixar vault.nfcv"**
2. Salve o arquivo em local seguro: Google Drive, OneDrive, pen drive, etc.

O arquivo `.nfcv` está **criptografado** — pode ser armazenado em qualquer lugar sem risco.

### Importar vault em outro dispositivo

1. Transfira o arquivo `.nfcv` para o novo dispositivo
2. Abra o NFC Vault → botão ⬇️ → **"Selecionar arquivo"**
3. Escolha o `.nfcv`
4. Desbloqueie normalmente com a tag NFC ou a chave

### Usar em múltiplos dispositivos

Cada dispositivo tem seu próprio localStorage — você precisa importar o `.nfcv` manualmente quando houver atualizações. Sugestão de rotina:

```
Adicionar/editar senhas → Exportar .nfcv → Salvar no Google Drive → 
No outro dispositivo: importar o .nfcv atualizado
```

---

## Hospedar no GitHub Pages

Para acessar de qualquer lugar sem precisar carregar o arquivo:

1. Crie um repositório no GitHub (pode ser público — o código não contém segredos)
2. Renomeie `nfc_vault.html` para `index.html` e faça o upload
3. Vá em **Settings → Pages → Branch: main → Save**
4. Acesse em `https://seu-usuario.github.io/nome-do-repositorio`

> ⚠️ **Nunca faça upload do arquivo `.nfcv`** no repositório público. Suba apenas o `index.html`.

### Instalar como app no Android (PWA)

1. Acesse a URL do GitHub Pages no Chrome
2. Toque no menu (⋮) → **"Adicionar à tela inicial"**
3. O vault aparecerá como um app na sua tela inicial

---

## Segurança

| Item | Detalhes |
|---|---|
| Algoritmo | AES-256-GCM (padrão militar) |
| Implementação | Web Crypto API nativa do navegador |
| Chave | 256 bits gerados por `crypto.getRandomValues` |
| IV | 96 bits aleatórios por operação de criptografia |
| Dependências externas | Nenhuma |
| Dados enviados a servidores | Nenhum |

### O que acontece se eu perder a tag NFC?

Se você tiver a chave salva em outro lugar (anotada, no celular, etc.), pode usá-la manualmente para desbloquear e gravar em uma nova tag.  
Se perdeu a tag **e** não tem a chave salva: as senhas não podem ser recuperadas.

**Recomendação:** salve a chave de 64 caracteres em um local seguro além da tag (ex: papel guardado, gerenciador de senhas de outro dispositivo).

---

## Arquivos do projeto

```
/
├── index.html     → o app completo (interface + criptografia)
└── README.md      → este documento
```

O arquivo `.nfcv` gerado pelo app **não deve ser versionado** — adicione ao `.gitignore`:

```
*.nfcv
```

---

## Tecnologias utilizadas

- **Web Crypto API** — criptografia AES-256-GCM nativa
- **Web NFC API** — leitura de tags NFC (Chrome Android 89+)
- **localStorage** — armazenamento local no navegador
- HTML + CSS + JavaScript puro — zero dependências, zero frameworks
