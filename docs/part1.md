# Part 1: Initial System Setup

Before you begin installing MkDocs, it's a good practice to ensure your **Ubuntu system** is up to date and that you have the necessary core tools ready. 

You will perform all of the following steps in your **terminal**.

---

## 1. Update and Upgrade System Packages

First, update your system's package list and upgrade any outdated packages. This ensures you're working with the latest versions of system software, which can prevent conflicts.

```bash
sudo apt update && sudo apt upgrade -y 
```

## 2. Verify Python Installation

MkDocs is a _Python-based_ application, so you need to confirm that Python 3 is installed. 

```bash
python3 --version
```
>Ubuntu typically comes with Python pre-installed, but it's a good idea to verify the version.

## 3. Check for and Install pip

`pip` is the standard package installer for Python and is essential for installing MkDocs.Check if it's already on your system.

```sh
pip --version
```
If `pip` is already installed, the command will display its version but, if you receive an _error like "command not found,"_ you'll need to install it.

Use the following command to install `pip` : 

```shell
sudo apt install python3-pip -y
```

>After installation, run `pip --version` again to confirm it's installed correctly.

## 4. Install Visual Studio Code

Visual Studio Code (VS Code) is used as the code editor  and terminal interface to work on the MkDocs project. 

If you don’t have it installed already, download and install it from the official website:
👉 [Download VS Code for Ubuntu](https://code.visualstudio.com/Download)


!!! note ""

    After you install VS Code, verify the `code` command is available in your terminal by opening a new terminal and typing `code --version`. 
    If the command isn't found, you'll need to add it to your system's PATH.

    ??? note "Here's how:"

        1. Launch Visual Studio Code.
        2. Open the Command Palette by pressing `Ctrl+Shift+P`.
        3. Type `Shell Command: Install 'code' command in PATH`.
        4. Hit Enter to run the command.
        >This will allow you to use the `code .` command later in the tutorial.


With these foundational steps complete, your system is now ready for the MkDocs installation.


---
⬅️ **Previous:** [Home](index.md) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ➡️ **Next:** [Create Project Directory](part2.md)

