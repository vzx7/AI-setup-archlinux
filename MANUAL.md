## STEP 0. Basic system
Updating the system:
```sh
sudo pacman -Syu
```
Install basic utilities:
```sh
sudo pacman -S git curl wget unzip base-devel htop btop neovim
```
## STEP 1. Setting up swap (MANDATORY)
If there is swap, you can skip this step.
Zram installation:
```sh
sudo pacman -S zram-generator
```
Create the config:
```sh
sudo nano /etc/systemd/zram-generator.conf
```
Insert:
```ini
[zram0]
zram-size = ram / 2
compression-algorithm = zstd
```
Launch:
```sh
sudo systemctl daemon-reexec
sudo systemctl start systemd-zram-setup@zram0
```
Check:
```sh
swapon --show
```
## STEP 2. CPU optimization
```sh
sudo pacman -S cpupower
sudo systemctl enable --now cpupower
```
Create config:
```sh
sudo nano /etc/default/cpupower
```
Insert:
```ini
governor='performance'
```
Apply:
```sh
sudo systemctl restart cpupower
```
## STEP 3. Install Ollama
```sh
curl -fsSL https://ollama.com/install.sh | sh
```
check:
```sh
ollama --version
```
Create start script:
```sh
nano ~/start-ollama.sh
```
Insert:
```sh
#!/bin/bash
pkill -f "ollama serve"

# server up
/usr/local/bin/ollama serve >/tmp/ollama.log 2>&1 &

# Check server
sleep 2
if curl -s http://127.0.0.1:11434 >/dev/null; then
    echo "Ollama server started successfully!"
else
    echo "Ollama launch error. Check the logs: /tmp/ollama.log"
fi
```
```sh
chmod +x ~/start-ollama.sh
```
## STEP 4. Installation of models
Set three
```sh
ollama pull qwen2.5:7b
ollama pull qwen:1.8b
ollama pull deepseek-coder:6.7b
```
Check:
```sh
ollama list
```
Test:
```sh
ollama run qwen2.5:7b
```
## STEP 5. Optimizing Ollama for CPU
Create the config:
```sh
mkdir -p ~/.ollama
nano ~/.ollama/config
```
Insert:
```ini
OLLAMA_NUM_THREADS=12
OLLAMA_MAX_LOADED_MODELS=2
OLLAMA_KEEP_ALIVE=5m
```
## STEP 6: Install Visual Studio Code
```sh
sudo pacman -S code
```
## STEP 7. Install Continue
Open VS Code:
```sh
code
```
Next:

Extensions (Ctrl+Shift+X)
Find: Continue
Install
## ШАГ 8. Конфиг Continue
Create a file:
```sh
mkdir -p ~/.continue
nano ~/.continue/config.yaml
```
Insert:
```yaml
name: Local Config
version: 1.0.0
schema: v1
models:
  - name: Qwen 1.8 Fast
    provider: ollama
    model: qwen:1.8b
    roles:
      - chat
      - autocomplete   # быстрые автодополнения
  - name: Qwen 2.5 Main
    provider: ollama
    model: qwen2.5:7b
    roles:
      - chat           # сложные вопросы
      - edit           # редактирование текста
  - name: Deepseek Coder
    provider: ollama
    model: deepseek-coder:6.7b
    roles:
      - apply          # код / генерация программ
  - name: Nomic Embed
    provider: ollama
    model: nomic-embed-text:latest
    roles:
      - embed          # векторные эмбеддинги
```
## STEP 9. Check
In VS Code:

1. Open any folder with code
2. Press Ctrl + I
3. Write:

```ini
Explain this project
```

Done!