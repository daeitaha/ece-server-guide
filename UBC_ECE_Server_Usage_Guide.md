# UBC ECE Group Server Usage Guide

---

## Prerequisites

Before accessing the server from off-campus, you must be connected to the **UBC VPN**. Ensure your VPN connection is active throughout your session.

---

## 1. Recommended Development Environment

We strongly recommend using **Visual Studio Code** with the **Remote - SSH** extension for streamlined development. This setup enables you to edit files on the remote server with the convenience of your local editor, providing syntax highlighting, IntelliSense, and integrated debugging.

---

## 2. Connecting to the Server

### 2.1 Initial Gateway Connection

Open your terminal (either within VS Code or standalone) and connect to the ECE gateway:

```bash
ssh <username>@ssh.ece.ubc.ca
```

Replace `<username>` with your ECE username. Enter your ECE password when prompted.

### 2.2 Accessing the Group Server

Once connected to the ECE gateway, access the group server by running:

```bash
ssh hlamarr
```

Enter your password again when prompted.

---

## 3. Visual Studio Code Setup

### 3.1 Installing Remote - SSH Extension

- Open VS Code and navigate to the Extensions marketplace
- Search for and install "Remote - SSH"
- Restart VS Code after installation

### 3.2 Connecting via Remote - SSH

1. Open the Command Palette (`Ctrl+Shift+P` or `Cmd+Shift+P`)
2. Select "Remote-SSH: Connect to Host..."
3. Click "Add New SSH Host"
4. Enter: `ssh <username>@ssh.ece.ubc.ca`
5. Select your SSH configuration file when prompted
6. Connect to the ECE gateway
7. Once connected, open a new terminal in VS Code and run `ssh hlamarr` to access the group server

---

## 4. SSH Public Key Authentication (Optional)

Setting up SSH key authentication eliminates the need to enter your password repeatedly, improving security and convenience.

### 4.1 Generate SSH Key Pair

On your local machine, generate a new SSH key pair:

```bash
ssh-keygen -t ed25519 -C "<your_email>"
```

Press Enter to accept the default location (`~/.ssh/id_ed25519`). Optionally, set a passphrase for additional security.

### 4.2 Copy Public Key to Gateway

Copy your public key to the ECE gateway server:

```bash
ssh-copy-id <username>@ssh.ece.ubc.ca
```

Replace `<username>` with your ECE username. Enter your password when prompted. Future connections will no longer require password authentication.

---

## 5. Installing Miniconda

If Conda is not already installed on your account, you'll need to install Miniconda:

1. Visit the official Miniconda documentation: https://www.anaconda.com/docs/getting-started/miniconda
2. Follow the installation instructions for Linux
3. After installation completes, restart your terminal session or run the initialization command provided

---

## 6. Conda Environment Management

After installing Conda, log out and log back in to ensure your environment is properly initialized.

### 6.1 Creating a New Environment

```bash
conda create -n myenv python=3.10
```

Replace `myenv` with your desired environment name and adjust the Python version as needed.

### 6.2 Activating and Deactivating Environments

To activate an environment:

```bash
conda activate myenv
```

To deactivate the current environment:

```bash
conda deactivate
```

### 6.3 Installing Packages

Install packages using either Conda or pip:

```bash
conda install numpy
```

```bash
pip install torch
```

### 6.4 Best Practices

- **One environment per project:** Create separate environments for different projects to prevent dependency conflicts
- **Avoid global installation:** Do not install packages in the `base` environment; use project-specific environments instead
- **Export environment configurations:** Regularly export your environment for reproducibility:

```bash
conda env export > environment.yml
```

---

## 7. Using Screen for Persistent Sessions

Screen allows you to run long-running processes that persist even after disconnecting from SSH. This is essential for training models or running lengthy computations.

### 7.1 Starting a New Session

```bash
screen
```

### 7.2 Detaching from a Session

To detach from a screen session while leaving it running in the background:

```
Ctrl+A, then press D
```

### 7.3 Listing Active Sessions

To view all running screen sessions:

```bash
screen -ls
```

### 7.4 Reattaching to a Session

To reconnect to a detached session:

```bash
screen -r <session_name>
```

If there's only one session, you can simply use `screen -r` without specifying a name.

---

## 8. Checking GPU Availability

Before starting computationally intensive tasks, verify GPU availability and current usage:

```bash
nvidia-smi
```

This command displays active processes, GPU utilization, memory usage, and available GPUs. Always check this before launching GPU-intensive workloads to be considerate of other users.

---

## 9. Running Python and MATLAB Code

Once you have confirmed GPU availability and started a screen session, you can execute your computational tasks.

### 9.1 Running Python Scripts

Execute a Python script within your activated Conda environment:

```bash
python your_script.py
```

### 9.2 Running MATLAB Scripts

For MATLAB scripts in command-line mode:

```bash
matlab -nodisplay -r "run('your_script.m'); exit;"
```

The `-nodisplay` flag runs MATLAB without a graphical interface, and `exit;` ensures MATLAB closes after completing the script.

---

## Quick Reference

### Common Workflow

```bash
# 1. Connect to gateway
ssh <username>@ssh.ece.ubc.ca

# 2. Connect to group server
ssh hlamarr

# 3. Start a screen session
screen

# 4. Activate your environment
conda activate myenv

# 5. Check GPU availability
nvidia-smi

# 6. Run your code
python your_script.py

# 7. Detach from screen (Ctrl+A, then D)

# 8. Later, reattach to check progress
screen -r
```

---

**For additional support, contact your system administrator or refer to the ECE IT documentation.**
