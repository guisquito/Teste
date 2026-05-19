# Dashboard Tributário — Instalação no iPhone via Capacitor

## Pré-requisitos (no seu Mac)

- **macOS** com Xcode instalado (App Store, gratuito, ~7 GB)
- **Node.js** v18+ — baixe em https://nodejs.org  
- **CocoaPods** — terminal: `sudo gem install cocoapods`
- **Apple Developer Account** (gratuito para testar no seu próprio iPhone)

---

## Passo a Passo

### 1. Clone o repositório (ou copie a pasta)

```bash
git clone https://github.com/guisquito/teste.git
cd teste
git checkout claude/access-mac-projects-Gox3c
```

### 2. Instale as dependências npm

```bash
npm install
```

### 3. Adicione a plataforma iOS

```bash
npx cap add ios
```

Isso cria a pasta `ios/` com o projeto Xcode.

### 4. Copie os arquivos web para o iOS

```bash
npx cap sync ios
```

### 5. Abra o Xcode

```bash
npx cap open ios
```

O Xcode abrirá automaticamente com o projeto `App.xcworkspace`.

### 6. Configure o Signing no Xcode

1. No painel esquerdo, clique em **App** (ícone azul)
2. Aba **Signing & Capabilities**
3. Em **Team**, selecione sua Apple ID / Developer Account
4. O Bundle Identifier já está configurado: `br.com.dashboardtributario.app`

### 7. Conecte seu iPhone

- Conecte o iPhone com cabo USB
- No iPhone: confirme "Confiar neste computador"
- No Xcode: selecione seu iPhone na lista de dispositivos (topo da tela)

### 8. Build e instalar

- Pressione **⌘R** (ou o botão ▶ Play) no Xcode
- Aguarde o build (1–3 minutos na primeira vez)
- O app abre automaticamente no iPhone

### 9. Confiar no desenvolvedor (necessário apenas uma vez)

No iPhone:
1. **Ajustes → Geral → VPN e Gerenciamento de Dispositivo**
2. Toque no seu Apple ID / Developer
3. Toque em **Confiar em "[seu nome]"**

---

## Atualizar o app depois

Se você modificar o `www/index.html` e quiser atualizar o app:

```bash
npx cap sync ios
# Depois, rebuild no Xcode (⌘R)
```

---

## Ícone personalizado (opcional)

Para adicionar um ícone real ao app:

1. Crie uma imagem PNG 1024×1024 pixels
2. Use o site https://appicon.co para gerar todos os tamanhos
3. Substitua os arquivos em `ios/App/App/Assets.xcassets/AppIcon.appiconset/`

---

## Estrutura do projeto

```
├── www/
│   ├── index.html      ← App principal (Dashboard Tributário)
│   ├── sw.js           ← Service Worker (cache offline)
│   ├── manifest.json   ← PWA manifest
│   ├── icon-192.png    ← Ícone 192×192
│   └── icon-512.png    ← Ícone 512×512
├── ios/                ← Gerado por: npx cap add ios
├── package.json
└── capacitor.config.json
```

---

## Problemas comuns

| Erro | Solução |
|------|---------|
| `command not found: npx` | Instale Node.js primeiro |
| `pod: command not found` | `sudo gem install cocoapods` |
| Build falha no Xcode | Certifique-se de ter selecionado um Team em Signing |
| App não aparece no iPhone | Veja Passo 9 (confiar no desenvolvedor) |
| Fontes não carregam | Precisa de internet na primeira abertura (Google Fonts CDN) |
