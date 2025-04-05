# **Oh My Zsh Installer with Plugins**

This script automates the installation of **Oh My Zsh**, **Zsh autosuggestions**, and **Zsh syntax highlighting** on a new server. It also allows you to set Zsh as the default shell.

## **Features**
- Installs **Oh My Zsh**.
- Installs **Zsh autosuggestions** and **Zsh syntax highlighting** plugins.
- Optionally sets Zsh as the default shell.
---

## **Prerequisites**
Ensure your server has the following installed:
- `curl`
- `git`
- `zsh` (the script will install it if not already present)

---

## **Installation**
1. Clone this repository or download the script:
   ```bash
   git clone https://github.com/dx64x/omz.git
   cd omz
   ```

2. Make the script executable:
   ```bash
   chmod +x install_zsh.sh
   ```

3. Run the script with or without arguments:

### **Usage**
```bash
./install_zsh.sh [yes|no]
```

- **Arguments:**
  - `yes`: Install Zsh and set it as the default shell.
  - `no` (default): Install Zsh without changing the default shell.

**Examples:**

- Install Oh My Zsh and make it the default shell:
  ```bash
  ./install_zsh.sh yes
  ```

- Install Oh My Zsh without changing the default shell:
  ```bash
  ./install_zsh.sh no
  ```

- If no argument is passed, it defaults to `no`:
  ```bash
  ./install_zsh.sh
  ```

#### Install zsh-completions plugin

* Clone the repository inside your oh-my-zsh repo:

        git clone https://github.com/zsh-users/zsh-completions ${ZSH_CUSTOM:-${ZSH:-~/.oh-my-zsh}/custom}/plugins/zsh-completions

* (optional) Add it to `FPATH` in your `.zshrc` by adding the following line before `source "$ZSH/oh-my-zsh.sh"`:

        fpath+=${ZSH_CUSTOM:-${ZSH:-~/.oh-my-zsh}/custom}/plugins/zsh-completions/src


# Configuração do Zsh para o Usuário Root

## 1. Corrigindo as permissões e propriedade dos arquivos

Primeiro, vamos garantir que o root tenha as permissões adequadas para acessar e usar os arquivos de configuração do Zsh:

1. Conceda permissões de leitura para o root em todos os arquivos e diretórios dentro do **Oh My Zsh** e dos arquivos de configuração do Zsh:

    ```bash
    sudo chmod -R +r /home/ussene/.oh-my-zsh
    sudo chmod -R +r /home/ussene/.zsh
    ```

2. Altere a propriedade do diretório **Oh My Zsh** para o root, garantindo que o root tenha controle sobre esses arquivos:

    ```bash
    sudo chown -R root:root /home/ussene/.oh-my-zsh
    ```

3. Remova as permissões de gravação para **grupo** e **outros usuários** nos diretórios de configuração, para evitar problemas de segurança:

    ```bash
    sudo chmod -R g-w,o-w /home/ussene/.oh-my-zsh
    ```

## 2. Criando Links Simbólicos para o Root

Agora, vamos criar links simbólicos para garantir que o **root** tenha acesso aos diretórios e arquivos de configuração do Zsh.

1. Crie um link simbólico para o diretório **Oh My Zsh**:

    ```bash
    sudo ln -s /home/ussene/.oh-my-zsh /root/.oh-my-zsh
    ```

2. Crie links simbólicos para as pastas de **autosuggestions** e **syntax highlighting**:

    ```bash
    sudo ln -s /home/ussene/.zsh/zsh-autosuggestions /root/.zsh/zsh-autosuggestions
    sudo ln -s /home/ussene/.zsh/zsh-syntax-highlighting /root/.zsh/zsh-syntax-highlighting
    ```

## 3. Modificando o arquivo `.zshrc` do Root

Agora, vamos modificar o arquivo `~/.zshrc` do root para garantir que ele use o arquivo de configuração do seu usuário normal.

1. Abra o arquivo `~/.zshrc` do root para edição:

    ```bash
    sudo nano ~/.zshrc
    ```

2. No final do arquivo, adicione a seguinte linha para garantir que o arquivo `~/.zshrc` do seu usuário normal seja carregado:

    ```bash
    if [ -f /home/ussene/.zshrc ]; then
        source /home/ussene/.zshrc
    fi
    ```

3. Salve e feche o arquivo (`Ctrl + O` para salvar e `Ctrl + X` para sair no `nano`).

## 4. Aplicando as mudanças

Para garantir que as mudanças tenham efeito, execute o comando a seguir:

```bash
source ~/.zshrc
```

---

🎉

## **License**
This project is licensed under the [MIT License](LICENSE).
