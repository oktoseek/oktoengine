# Requisitos de Imagens para OktoEngine GitHub

Lista completa de imagens necessárias para a documentação do OktoEngine.

---

## 📸 Imagens Obrigatórias

### 1. Logo Principal
**Arquivo:** `okto_logo.png`  
**Uso:** Logo principal do OktoEngine no README  
**Tamanho recomendado:** 800x200px ou similar (proporção 4:1)  
**Formato:** PNG com fundo transparente  
**Onde é usado:** Topo do README.md

---

### 2. Logo Alternativo
**Arquivo:** `okto_logo2.png`  
**Uso:** Logo alternativo (opcional, pode ser o mesmo do OktoScript)  
**Tamanho recomendado:** 800x200px  
**Formato:** PNG  
**Onde é usado:** README.md (seguindo padrão OktoScript)

---

### 3. Screenshot - Comando `okto validate`
**Arquivo:** `terminal-validate.png`  
**Descrição:** Screenshot do terminal mostrando `okto validate` sendo executado  
**O que mostrar:**
- Comando `okto validate` sendo executado
- Saída de validação bem-sucedida
- Mensagens de sucesso e resumo

**Exemplo do que capturar:**
```
PS D:\projects\my-project> okto validate

🐙 OktoEngine v0.1
🔍 Validating OktoScript file: "scripts/train.okt"
📄 File: "scripts/train.okt"
📄 Size: 382 bytes
📄 Lines: 31

✔ File parsed successfully

📋 Validation Results:
✅ Validation passed! No errors or warnings.

📊 Summary:
  Project: my-project
  ENV: Configured
  Dataset: dataset/train.jsonl
  Model: gpt2
  Training: 5 epochs, batch size 32
  Export: ["okm"]
```

---

### 4. Screenshot - Comando `okto train`
**Arquivo:** `terminal-train.png`  
**Descrição:** Screenshot do terminal mostrando `okto train` em execução  
**O que mostrar:**
- Comando `okto train` sendo executado
- Environment check
- Progresso do treinamento (barra de progresso)
- Métricas em tempo real
- Mensagem de sucesso

**Exemplo do que capturar:**
```
PS D:\projects\my-project> okto train

🐙 OktoEngine v0.1
📄 Reading: "scripts/train.okt"

📊 Environment Check:
  ✔ Runtime: Python 3.14.0
  ✔ GPU: NVIDIA GeForce RTX 4070
  ✔ RAM: 63GB (40GB available)
  ✔ Platform: windows

📦 Checking dependencies...
  ✔ All dependencies available

🚀 Starting training pipeline...

Epoch 1/5: 100%|████████████| 500/500 [02:15<00:00, 3.70it/s]
  Loss: 2.345 → 1.892
  Learning Rate: 5e-5
  GPU Memory: 8.2GB / 12GB

✅ Training completed successfully!
📁 Output: runs/my-project/
```

---

### 5. Screenshot - Comando `okto doctor`
**Arquivo:** `terminal-doctor.png`  
**Descrição:** Screenshot do terminal mostrando `okto doctor`  
**O que mostrar:**
- Comando `okto doctor` sendo executado
- Diagnóstico completo do sistema
- Todas as verificações (GPU, CUDA, RAM, etc.)
- Status de dependências

**Exemplo do que capturar:**
```
PS D:\projects> okto doctor

🐙 OktoEngine v0.1 - System Diagnostics

🖥️  Platform: Windows
💾 RAM: 63GB total, 40GB available
⚙️  CPU: 32 cores
🎮 GPU: Checking...
  ✔ GPU found: NVIDIA GeForce RTX 4070 Laptop GPU
🔧 CUDA: Checking...
  ✔ CUDA available: 576.02
🔧 Runtime: Checking...
  ✔ Runtime available: Python 3.14.0
📦 Dependencies: Checking...
  ✔ All required packages installed

✅ Diagnostics complete
```

---

### 6. Screenshot - Modo Debug
**Arquivo:** `terminal-debug.png`  
**Descrição:** Screenshot do terminal mostrando `okto train --debug`  
**O que mostrar:**
- Comando `okto train --debug` sendo executado
- Logs de debug detalhados
- Parsing logs
- Execution flow

**Exemplo do que capturar:**
```
PS D:\projects\my-project> okto train --debug

🐙 OktoEngine v0.1
📄 Reading: "scripts/train.okt"

DEBUG: Starting parse_oktoscript. Input preview: '# okto_version: "1.0" PROJECT...'
DEBUG: Parsed version: Some("1.0")
DEBUG: Parsed project: my-project
DEBUG: After PROJECT, remaining input: 'ENV { accelerator: "gpu"...'
DEBUG: Attempting to parse ENV block...
DEBUG: Parsed ENV field: accelerator = gpu
DEBUG: Parsed ENV field: precision = fp16
DEBUG: Successfully parsed ENV block with 5 fields
...
```

---

### 7. Screenshot - Comando `okto upgrade`
**Arquivo:** `terminal-upgrade.png`  
**Descrição:** Screenshot do terminal mostrando `okto upgrade`  
**O que mostrar:**
- Comando `okto upgrade` sendo executado
- Verificação de atualizações
- Download em progresso (barra de progresso)
- Mensagem de sucesso

**Exemplo do que capturar:**
```
PS D:\projects> okto upgrade

🐙 OktoEngine Upgrader
Current version: 0.1.0
🔍 Checking for updates...

📦 Downloading OktoEngine v0.2.0...
████████████████████ 100% [00:15<00:00]

✅ Updated successfully to v0.2.0
```

---

### 8. Screenshot - Comando `okto about`
**Arquivo:** `terminal-about.png`  
**Descrição:** Screenshot do terminal mostrando `okto about`  
**O que mostrar:**
- Comando `okto about` sendo executado
- Informações sobre OktoScript e OktoEngine
- Links e referências

---

### 9. Screenshot - Comando `okto init`
**Arquivo:** `terminal-init.png`  
**Descrição:** Screenshot do terminal mostrando `okto init`  
**O que mostrar:**
- Comando `okto init my-project` sendo executado
- Mensagem de sucesso
- Estrutura de pastas criada

---

### 10. Screenshot - Erro com Debug (Opcional)
**Arquivo:** `terminal-error-debug.png`  
**Descrição:** Screenshot mostrando erro com debug mode ativado  
**O que mostrar:**
- Erro ocorrendo
- Debug logs mostrando onde falhou
- Mensagens de erro detalhadas

---

## 📋 Checklist de Imagens

Use esta checklist ao capturar as imagens:

- [ ] `okto_logo.png` - Logo principal
- [ ] `okto_logo2.png` - Logo alternativo (opcional)
- [ ] `terminal-validate.png` - Validação
- [ ] `terminal-train.png` - Treinamento
- [ ] `terminal-doctor.png` - Diagnóstico
- [ ] `terminal-debug.png` - Modo debug
- [ ] `terminal-upgrade.png` - Atualização
- [ ] `terminal-about.png` - Informações
- [ ] `terminal-init.png` - Inicialização
- [ ] `terminal-error-debug.png` - Erro com debug (opcional)

---

## 🎨 Especificações Técnicas

### Formato
- **Tipo:** PNG (preferido) ou JPEG
- **Qualidade:** Alta resolução
- **Tamanho máximo:** 2MB por imagem

### Dimensões
- **Screenshots de terminal:** 1920x1080 ou maior
- **Logos:** Proporção 4:1 (ex: 800x200px)
- **Banners:** Proporção 16:9 (ex: 1920x1080px)

### Estilo
- **Fundo:** Escuro (terminal) ou claro (dependendo do tema)
- **Texto:** Legível e nítido
- **Cores:** Manter cores originais do terminal
- **Emojis:** Mostrar emojis se visíveis no terminal

---

## 📝 Como Capturar

### Windows
1. Abra o terminal (PowerShell ou CMD)
2. Execute o comando
3. Use `Win + Shift + S` para captura de tela
4. Ou use ferramenta de screenshot
5. Salve como PNG

### Linux
1. Use `gnome-screenshot` ou `scrot`
2. Ou `Shift + Print Screen`
3. Salve como PNG

### macOS
1. Use `Cmd + Shift + 4` para captura de área
2. Ou `Cmd + Shift + 3` para tela inteira
3. Salve como PNG

---

## 📍 Onde Usar Cada Imagem

### README.md
- `okto_logo.png` - Topo do README
- `okto_logo2.png` - Logo alternativo (se usado)
- `terminal-train.png` - Seção de exemplos
- `terminal-validate.png` - Seção de validação

### docs/GETTING_STARTED.md
- `terminal-init.png` - Seção de inicialização
- `terminal-validate.png` - Seção de validação
- `terminal-train.png` - Seção de treinamento

### docs/CLI_REFERENCE.md
- Screenshots de cada comando nas respectivas seções

### docs/DEBUG_GUIDE.md
- `terminal-debug.png` - Exemplo de debug mode
- `terminal-error-debug.png` - Exemplo de erro com debug

---

## ✅ Checklist Final

Antes de enviar as imagens, verifique:

- [ ] Todas as imagens têm os nomes corretos
- [ ] Imagens estão em formato PNG ou JPEG
- [ ] Texto está legível
- [ ] Cores estão corretas
- [ ] Tamanho está adequado (< 2MB)
- [ ] Resolução é suficiente (1920x1080+)
- [ ] Screenshots mostram comandos reais funcionando

---

## 📧 Envio

Envie as imagens com os nomes exatos listados acima para:
- **Email:** service@oktoseek.com
- **Ou adicione diretamente na pasta `assets/`**

---

**Nota:** Se alguma imagem não estiver disponível, podemos usar placeholders temporários ou criar screenshots de exemplo.

