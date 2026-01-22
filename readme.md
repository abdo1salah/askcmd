# askcmd 🤖💻

**Turn natural language into Linux commands instantly.**

`askcmd` is a lightweight, AI-powered terminal utility that converts English descriptions (e.g., "find all large PDFs") into executable Bash commands. It uses **Ollama** locally to ensure privacy and speed.

> **Safety First:** Unlike other AI tools that execute code blindly, `askcmd` generates the command and **copies it to your clipboard**. You paste it, review it, and execute it when ready.

## 🚀 Features

* **⚡ Local AI:** Runs entirely offline using Ollama (default: `qwen2.5-coder`).
* **📋 Clip-First Workflow:** Commands are copied to the clipboard automatically.
* **🧠 Context Aware:** The AI knows your **current working directory**, so it can generate relative paths correctly (e.g., "zip this folder").
* **🐧 Distro Optimized:** Optimized for Debian/Ubuntu based systems (handles `apt`, `wl-copy`, `xclip` automatically).
* **🛡️ Safety Guardrails:** Refuses to generate dangerous commands (like `rm -rf /`) without warnings.

## 🛠️ Prerequisites

1. **Linux** (Ubuntu/Debian recommended, but works on others).
2. **Python 3.8+**
3. **Ollama** installed and running.
* *Install:* `curl -fsSL https://ollama.com/install.sh | sh`



## 📦 Installation

### 1. Install System Dependencies

We need a clipboard utility. Even if you use Wayland, we install `xclip` as a robust fallback.

```bash
sudo apt update
sudo apt install xclip

```

### 2. Pull the AI Model

We recommend **Qwen 2.5 Coder (3B)** for the best balance of speed and accuracy.

```bash
ollama pull qwen2.5-coder:3b

```

### 3. Setup the Script

Clone this repo (or create the file manually).

```bash
# 1. Create a bin directory if you don't have one
mkdir -p ~/bin

# 2. Download the script (assuming you are pasting the code provided previously)
nano ~/bin/askcmd

# 3. Make it executable
chmod +x ~/bin/askcmd

# 4. Add ~/bin to your PATH (if not already there)
echo 'export PATH="$HOME/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc

```

### 4. Install Python Libraries

```bash
pip install langchain-ollama langchain-core

```

## 💡 Usage

Open your terminal and type `askcmd` followed by your request.

**Example 1: File Search**

```bash
askcmd find all jpg images larger than 5MB in this folder

```

*Output:* `✔ Copied to clipboard: find . -name "*.jpg" -size +5M`

**Example 2: System Admin**

```bash
askcmd check which process is using port 8080

```

*Output:* `✔ Copied to clipboard: sudo lsof -i :8080`

**Example 3: Complex Archives**

```bash
askcmd compress the current folder into a tar.gz named backup excluding the .git folder

```

*Output:* `✔ Copied to clipboard: tar --exclude='.git' -czf backup.tar.gz .`

---

**Just press `Ctrl+Shift+V` (or `Ctrl+V`) to paste and run!**

## ⚙️ Configuration

### Changing the Model

If you have a powerful machine (16GB+ RAM), you can switch to the 7B model for higher accuracy.

1. Pull the model: `ollama pull qwen2.5-coder:7b`
2. Edit the script (`nano ~/bin/askcmd`):
```python
model = ChatOllama(model="qwen2.5-coder:7b", temperature=0)


MIT License. Feel free to modify and share!
