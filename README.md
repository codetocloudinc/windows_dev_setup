# 💻 Windows Laptop Setup for Development and AI Tasks (Leveraging WSL)

---

## 🛠️ 1. Setting Up WSL
- **Enable WSL2 on Windows**:  
  Open PowerShell as Administrator and run:  
  ```powershell
  wsl --install
  ```
- **Install your preferred Linux distribution** (e.g., Ubuntu):  
  ```powershell
  wsl --install -d Ubuntu
  ```
- **Update the installed Linux distribution** (inside WSL):  
  ```bash
  sudo apt update && sudo apt upgrade -y
  ```

---

## 🔧 2. Development Tools via WSL

### 🏗️ a. Terraform
- **Install Terraform CLI**:  
  ```bash
  sudo apt install -y wget unzip
  wget https://releases.hashicorp.com/terraform/$(curl -s https://releases.hashicorp.com/terraform/ | grep -oP '\d+\.\d+\.\d+' | head -1)/terraform_$(curl -s https://releases.hashicorp.com/terraform/ | grep -oP '\d+\.\d+\.\d+' | head -1)_linux_amd64.zip
  unzip terraform_*.zip
  sudo mv terraform /usr/local/bin/
  ```

### 🧱 b. Bicep
- **Install Bicep using Azure CLI**:  
  First, install the Azure CLI:  
  ```bash
  curl -sL https://aka.ms/InstallAzureCLIDeb | sudo bash
  az bicep install
  ```

### 🌱 c. OpenTofu
- **Install OpenTofu (an open-source alternative to Terraform)**:  
  ```bash
  curl -sSLf https://apt.opentofu.org/gpg | sudo gpg --dearmor -o /usr/share/keyrings/opentofu-archive-keyring.gpg
  echo "deb [signed-by=/usr/share/keyrings/opentofu-archive-keyring.gpg] https://apt.opentofu.org stable main" | sudo tee /etc/apt/sources.list.d/opentofu.list > /dev/null
  sudo apt update && sudo apt install -y opentofu
  ```

### 🎨 d. Oh My Posh
- **Install Oh My Posh CLI in WSL**:  
  ```bash
  sudo apt install -y wget
  wget https://github.com/JanDeDobbeleer/oh-my-posh/releases/latest/download/posh-linux-amd64
  sudo mv posh-linux-amd64 /usr/local/bin/oh-my-posh
  sudo chmod +x /usr/local/bin/oh-my-posh
  ```
- **Install a Nerd Font for glyph support**:  
  ```bash
  mkdir -p ~/.local/share/fonts
  cd ~/.local/share/fonts
  wget https://github.com/ryanoasis/nerd-fonts/releases/download/v2.3.3/FiraCode.zip
  unzip FiraCode.zip
  fc-cache -fv
  ```
- **Add Oh My Posh configuration to your shell**:  
  ```bash
  echo 'eval "$(oh-my-posh init bash)"' >> ~/.bashrc
  ```

### 🛠️ e. Linux Utilities for Development
- **Install essential utilities and tools**:  
  ```bash
  sudo apt install -y build-essential git curl wget unzip
  ```

---

## 🤖 3. AI Tools for Azure Development via WSL

### 🐍 a. Python Environment
- **Install Python and pip**:  
  ```bash
  sudo apt install -y python3 python3-pip
  ```
- **Install Azure SDKs for Python**:  
  ```bash
  pip3 install azure-storage-blob azure-mgmt-resource azure-ai-formrecognizer
  ```

### ☁️ b. Azure CLI for AI Management
- **Already installed earlier**. Use it to manage Azure resources:  
  ```bash
  az login
  ```

---

## 🧹 4. Removing Ads and Bloatware (Windows Side)

### 🛠️ a. Manual Steps
- Open **Settings > Apps** to uninstall unnecessary applications.
- Disable ads:  
  - **Settings > Personalization > Start**: Turn off “Show suggestions.”  
  - **Settings > Privacy > General**: Disable ad-related options.

### 🧹 b. WSL PowerShell Command for Bloat Removal
- **Run this command from WSL**:  
  ```bash
  powershell.exe "Get-AppxPackage -AllUsers | Remove-AppxPackage"
  ```

### ⚙️ c. Automated Bloat Removal
- **Use the [Win11Debloat](https://github.com/Raphire/Win11Debloat) script**:  
  Inside WSL, download and execute it:  
  ```bash
  wget https://raw.githubusercontent.com/Raphire/Win11Debloat/main/Win11Debloat.ps1
  powershell.exe -File ./Win11Debloat.ps1
  ```

---

## 🤖 5. Automation via Script
- **Automate the setup in WSL with this script**:  
  ```bash
  # Update and install tools
  sudo apt update && sudo apt upgrade -y
  sudo apt install -y wget unzip git python3 python3-pip curl build-essential

  # Install Terraform
  wget https://releases.hashicorp.com/terraform/$(curl -s https://releases.hashicorp.com/terraform/ | grep -oP '\d+\.\d+\.\d+' | head -1)/terraform_$(curl -s https://releases.hashicorp.com/terraform/ | grep -oP '\d+\.\d+\.\d+' | head -1)_linux_amd64.zip
  unzip terraform_*.zip
  sudo mv terraform /usr/local/bin/

  # Install OpenTofu
  curl -sSLf https://apt.opentofu.org/gpg | sudo gpg --dearmor -o /usr/share/keyrings/opentofu-archive-keyring.gpg
  echo "deb [signed-by=/usr/share/keyrings/opentofu-archive-keyring.gpg] https://apt.opentofu.org stable main" | sudo tee /etc/apt/sources.list.d/opentofu.list > /dev/null
  sudo apt update && sudo apt install -y opentofu

  # Install Azure CLI and Bicep
  curl -sL https://aka.ms/InstallAzureCLIDeb | sudo bash
  az bicep install

  # Install Oh My Posh
  wget https://github.com/JanDeDobbeleer/oh-my-posh/releases/latest/download/posh-linux-amd64
  sudo mv posh-linux-amd64 /usr/local/bin/oh-my-posh
  sudo chmod +x /usr/local/bin/oh-my-posh
  echo 'eval "$(oh-my-posh init bash)"' >> ~/.bashrc

  # Install Python Azure SDKs
  pip3 install azure-storage-blob azure-mgmt-resource azure-ai-formrecognizer
  ```
---

This version uses icons and formatting to make the document easier to read and visually engaging. Let me know if you need further adjustments! 🚀