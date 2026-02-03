# Setup New Machine Guide

## Quick Setup Checklist

สำหรับเมื่อย้ายไปเครื่องใหม่หรือ setup เครื่องใหม่

---

## 1. Install Essential Software

### Git
```bash
# Windows (via winget)
winget install Git.Git

# macOS
brew install git

# Linux
sudo apt install git
```

### Node.js (LTS)
```bash
# Windows (via winget)
winget install OpenJS.NodeJS.LTS

# macOS
brew install node@20

# Linux (via nvm - recommended)
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.0/install.sh | bash
nvm install 20
nvm use 20
```

### VS Code
```bash
# Windows
winget install Microsoft.VisualStudioCode

# macOS
brew install --cask visual-studio-code

# Linux
sudo snap install code --classic
```

---

## 2. Configure Git

```bash
# Set identity
git config --global user.name "Your Name"
git config --global user.email "your@email.com"

# Set default branch
git config --global init.defaultBranch main

# Set editor
git config --global core.editor "code --wait"
```

---

## 3. Generate SSH Key

```bash
# Generate key
ssh-keygen -t ed25519 -C "your@email.com"

# Start ssh-agent
eval "$(ssh-agent -s)"

# Add key
ssh-add ~/.ssh/id_ed25519

# Copy public key
# Windows
clip < ~/.ssh/id_ed25519.pub
# macOS
pbcopy < ~/.ssh/id_ed25519.pub
# Linux
cat ~/.ssh/id_ed25519.pub
```

Add key to GitHub: https://github.com/settings/keys

---

## 4. Install Claude Code

```bash
# Install globally
npm install -g @anthropic-ai/claude-code

# Verify
claude --version

# Login
claude login
```

---

## 5. VS Code Extensions

### Essential
- ESLint
- Prettier
- GitLens
- Thunder Client (API testing)

### Framework-specific
- **React**: ES7+ React/Redux/React-Native snippets
- **Vue**: Vue - Official
- **Tailwind**: Tailwind CSS IntelliSense
- **Prisma**: Prisma

Install from command line:
```bash
code --install-extension dbaeumer.vscode-eslint
code --install-extension esbenp.prettier-vscode
code --install-extension eamodio.gitlens
code --install-extension rangav.vscode-thunder-client
```

---

## 6. Clone This Template

```bash
# Clone template
git clone https://github.com/goffeeai/claude-vibe-coding-starter-template.git

# Or use in new project
mkdir my-project && cd my-project
git clone https://github.com/goffeeai/claude-vibe-coding-starter-template.git .template
cp -r .template/.claude .template/CLAUDE.md ./
rm -rf .template
```

---

## 7. Optional: Additional Tools

### pnpm (faster npm)
```bash
npm install -g pnpm
```

### Bun (faster runtime)
```bash
# Windows
powershell -c "irm bun.sh/install.ps1|iex"

# macOS/Linux
curl -fsSL https://bun.sh/install | bash
```

### Docker
```bash
# Windows
winget install Docker.DockerDesktop

# macOS
brew install --cask docker

# Linux
curl -fsSL https://get.docker.com | sh
```

---

## 8. Project-specific Setup

เมื่อ clone โปรเจคใหม่:

```bash
# Install dependencies
npm install

# Copy environment file
cp .env.example .env.local

# Edit environment variables
code .env.local

# Run development server
npm run dev
```

---

## Troubleshooting

### npm permission issues
```bash
# Fix permissions
sudo chown -R $(whoami) ~/.npm
```

### SSH connection refused
```bash
# Check ssh-agent
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519

# Test connection
ssh -T git@github.com
```

### Port in use
```bash
# Find and kill process
# Windows
netstat -ano | findstr :3000
taskkill /PID <PID> /F

# macOS/Linux
lsof -i :3000
kill -9 <PID>
```
