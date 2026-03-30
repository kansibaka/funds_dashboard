WINDOWS 11 + WSL + DOCKER + SSH + GITHUB + VS CODE
----------------------------------------------------------------------------------------------------
OVERVIEW

This guide describes how to set up a clean, production-like development environment on Windows 11 using:
- WSL2 with Ubuntu
- Docker Desktop (WSL backend)
- VS Code with Remote - WSL
- GitHub authentication via SSH
- Projects stored inside the Linux filesystem
This setup ensures proper performance, correct Docker behavior, and professional workflow.
----------------------------------------------------------------------------------------------------
STEP 0 – INSTALL REQUIRED SOFTWARE (WINDOWS SIDE)

1. Install WSL
- Open PowerShell as Administrator and run:
    wsl --install
- Reboot if prompted.
    wsl --status
- Check the “Default Version”.
- If it is not 2, run:
    wsl --set-default-version 2
- Then verify installed distributions:
    wsl -l -v
- Ensure Ubuntu shows VERSION 2.
- If not, convert it:
    wsl --set-version Ubuntu 2
- If Ubuntu was not automatically installed:
    wsl --install -d Ubuntu
- Launch Ubuntu once and create your Linux username and password.

2. Install Docker Desktop
Download Docker Desktop from docker.com.
During installation:
- Enable WSL 2 backend
- Enable integration with Ubuntu
After installation:
Open Docker Desktop.
Go to Settings → Resources → WSL Integration.
Enable integration for Ubuntu.

3. Install Visual Studio Code
Download and install VS Code from code.visualstudio.com.
Install the following extensions:
- Remote - WSL (by Microsoft)
- Docker (optional but useful)
----------------------------------------------------------------------------------------------------
STEP 1 – ENTER WSL PROPERLY

Open Windows Terminal.
Run:
    wsl
You should see a prompt like:
    user@DESKTOP:~$
You are now inside Ubuntu.
Do not work inside /mnt/c/Users/...
Projects must live inside the Linux filesystem under /home.
----------------------------------------------------------------------------------------------------
STEP 2 – CREATE PROJECT DIRECTORY IN LINUX FILESYSTEM

Inside Ubuntu:
    mkdir -p ~/projects
    cd ~/projects
All development projects should be stored under:
    /home/yourusername/projects
Never store active development projects inside:
    /mnt/c/Users/...
----------------------------------------------------------------------------------------------------
STEP 3 – SET UP SSH FOR GITHUB (PER MACHINE)

Check whether an SSH key already exists:
    ls -al ~/.ssh
If no key exists, generate one:
    ssh-keygen -t ed25519 -C "your_email@example.com"
Press Enter to accept default file location.
Optionally set a passphrase.
Start the SSH agent:
    eval "$(ssh-agent -s)"
Add your key:
    ssh-add ~/.ssh/id_ed25519
Copy your public key:
    cat ~/.ssh/id_ed25519.pub
Copy the entire output.
Go to GitHub:
    Settings → SSH and GPG Keys → New SSH Key
Paste the key and save.
Test the connection:
    ssh -T git@github.com
Type "yes" if prompted to confirm authenticity.
Successful authentication should display:
    Hi yourusername! You've successfully authenticated, but GitHub does not provide shell access.
Configuring Git identity inside WSL.
Inside Ubuntu, configure Git user identity:
    git config --global user.name "Your Name"
    git config --global user.email "your_email@example.com"
Verify:
    git config --global --list
This must match the email used in your GitHub account so commits are correctly attributed.
----------------------------------------------------------------------------------------------------
STEP 4 – CLONE PROJECT USING SSH

Inside ~/projects:
    git clone git@github.com:yourusername/yourrepo.git
    cd yourrepo
Verify remote:
    git remote -v
It must show:
    git@github.com:yourusername/yourrepo.git
If it shows https://, switch it:
    git remote set-url origin git@github.com:yourusername/yourrepo.git
----------------------------------------------------------------------------------------------------
STEP 5 – OPEN PROJECT IN VS CODE CORRECTLY

From inside the project directory in Ubuntu:
    code .
VS Code should open.
In the bottom-left corner, it must display: 
    WSL: Ubuntu
Open the integrated terminal in VS Code.
It must show:
    user@DESKTOP:~/projects/yourrepo$
If it shows PowerShell or a Windows path, you are not in WSL mode.
----------------------------------------------------------------------------------------------------
STEP 6 – VERIFY DOCKER INTEGRATION

Inside the VS Code terminal:
    docker ps
If no error appears, Docker is correctly integrated with WSL.
If you see a daemon error, verify that Docker Desktop is running and WSL integration is enabled.
----------------------------------------------------------------------------------------------------
STEP 7 – SANITY CHECKS

Run:
    pwd
It must display:
    /home/yourusername/projects/yourrepo
Run:
    git remote -v
It must show SSH URLs.
Run:
    docker ps
It must not show a connection error.
----------------------------------------------------------------------------------------------------
EXPECTED FINAL ARCHITECTURE

Windows 11
→ WSL2 (Ubuntu)
→ Docker Desktop using WSL backend
→ VS Code connected via Remote - WSL
→ GitHub authenticated via SSH
→ Projects stored inside Linux filesystem under /home

This provides:
- Proper Docker performance
- Correct file watching behavior
- Production-like Linux environment
- Secure GitHub authentication
- Reproducible machine-independent setup
----------------------------------------------------------------------------------------------------
MIGRATING TO A NEW WINDOWS 11 LAPTOP

Do not copy WSL or Docker state.
On the new laptop:
- Install WSL
- Install Ubuntu
- Install Docker Desktop
- Install VS Code + Remote - WSL
- Generate a new SSH key
- Add SSH key to GitHub
- Clone repository via SSH
- Open project using code .
- Verify Docker and Git
Your GitHub repository is the single source of truth.
----------------------------------------------------------------------------------------------------
END OF GUIDE
