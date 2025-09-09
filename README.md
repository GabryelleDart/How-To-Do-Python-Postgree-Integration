# 🐍💾 How-To-Do-Python-PostgreSQL-Integration

<intro>

---

## 📖 Sobre o Projeto
Este repositório tem como objetivo ajudar você a:  
✅ Entender o que é o **PostgreSQL**  
✅  

---
## 🐘 O que é o PostgreSQL?
O **PostgreSQL** (ou apenas *Postgres*) é um **banco de dados relacional**.  
Isso significa que ele armazena informações em **tabelas organizadas**, permitindo relacionar dados de forma lógica e eficiente.  

👉 Imagine uma planilha do Excel com várias abas (tabelas), mas muito mais poderosa, rápida e segura.  

### 🌟 Principais características:
- 🎯 **Gratuito e Open Source** – não precisa pagar licença  
- 🔐 **Seguro** – autenticação por senha e criptografia  
- 📈 **Escalável** – desde pequenos projetos até grandes empresas  
- 🧩 **Flexível** – suporta números, textos, JSON, geolocalização e muito mais  

### 🛠️ Onde é usado?
- Sistemas de gestão (ERP, CRM)  
- Aplicações web e APIs (Python, Java, Node.js...)  
- Ciência de dados e análise de grandes volumes  
- Aplicativos de celular que salvam informações de usuários  
- Plataformas como **Instagram** e **Spotify** usam bancos de dados relacionais semelhantes 🎵📸  

---

## ⚙️ Estrutura do Projeto
📂 Aqui você encontrará:  


---

## 🛠️ Como instalar o PostgreSQL no ambiente de desenvolvimento

### 🔑 Informações prévias
Ao instalar o PostgreSQL no seu computador, você terá:
- 🖥️ **Servidor PostgreSQL** → onde os dados ficam armazenados  
- ⌨️ **Cliente psql** → programa de linha de comando para interagir com o banco  
- 🎨 (Opcional) **pgAdmin** → interface gráfica para gerenciar o banco  

⚠️ **Segurança básica:**  
- O PostgreSQL cria um usuário administrador chamado **postgres**  
- Defina uma **senha forte** para ele  
- O arquivo `pg_hba.conf` controla conexões → use o método **md5** (senha criptografada) para acesso local  

---

### 💻 Instalação no Windows

#### 📥 Passo a passo
1. Acesse 👉 [PostgreSQL Download](https://www.postgresql.org/download/)
   
<img width="1919" height="910" alt="Captura de tela 2025-09-09 165154" src="https://github.com/user-attachments/assets/2cecbfd9-50f7-40f9-b562-2a0533cc8fc1" />

2. Clique em **Download the installer**
   
<img width="1919" height="899" alt="image" src="https://github.com/user-attachments/assets/c339ba4f-6f9e-46f7-9d4b-3836aa4d8b7c" />

3. Escolha sua versão e sistema operacional
<img width="1916" height="909" alt="image" src="https://github.com/user-attachments/assets/0ae0f12c-397b-4c94-83bc-3f0cda8c08b9" />

4. Execute o instalador e selecione os componentes:
   - ✅ PostgreSQL Server  
   - ✅ pgAdmin 4  
   - ✅ Command Line Tools
     
5. Defina a senha do usuário **postgres**  (é o "administrador do banco")
   
6. Deixe a porta padrão `5432` (a menos que já esteja em uso)
   
> **💡 Nota:** Normalmente o instalador sugerirá a porta `5432`, mas caso haja diferença, é porque esta porta já está sendo usada por outra aplicação.
>

7. Finalize a instalação 🎉  

#### 🔍 Testando
Abra o **Prompt de Comando (CMD)** e digite:
```bash
psql --version
```
>Caso o CMD não reconheça, adicione o caminho `C:\Program Files\PostgreSQL\<versão>\bin` às **variáveis de ambiente** do Windows.
>

---


### 🐧 Instalação no Linux (Ubuntu/Debian)

#### 📥 Passo a passo

1. Atualize os pacotes do sistema:
   
   ```bash
   sudo apt update && sudo apt upgrade -y
   ```
   
2. Instale o PostgreSQL e pacotes adicionais:
   
  ```bash
   sudo apt install postgresql postgresql-contrib -y
   ```
- postgresql: instala o servidor e cliente principal.
- postgresql-contrib: adiciona extensões úteis (JSON, criptografia, estatísticas etc).
  
3.Verifique se o serviço foi iniciado corretamente:

```bash
  sudo systemctl status postgresql
   ```
-Iniciar: sudo systemctl start postgresql

-Parar: sudo systemctl stop postgresql

-Reiniciar: sudo systemctl restart postgresql

###  🍎 Instalação no macOS

#### 📥 Instalação via Homebrew

1. Verifique se o Homebrew está instalado:
   ```bash
   brew --version
   ```
2. Instale o PostgreSQL:
  ```bash
  brew update
  brew install postgresql
   ```
3.Inicie o serviço automaticamente em segundo plano:
```bash
  brew services start postgresql
   ```
3.Teste se está funcionando:
```bash
 psql --version
   ```
-------------
## Configurar o PostgreSQL para acesso local seguro
### 📝 O que é “Acesso Local Seguro”?

O **acesso local seguro** significa que o banco de dados só pode ser acessado do próprio computador (localhost) e que **exige autenticação** (senha) para entrar.  

Isso evita que pessoas de fora da sua rede consigam se conectar ao banco sem permissão.  
Mesmo em ambientes de desenvolvimento, é importante garantir que:
- Somente usuários autorizados acessem o banco.
- Senhas sejam usadas para conexões.
- As permissões sejam adequadas para cada usuário.


### 💡 Como funciona?

O PostgreSQL utiliza um arquivo chamado **`pg_hba.conf`** (Host-Based Authentication) que define:
1. Quem pode acessar o banco.
2. De onde podem acessar (localhost, IPs específicos, redes).
3. Como se autenticar (senha, certificado, trust sem senha etc).

### 🛡️ Configuração Recomendada para Acesso Local
1. Localize o arquivo **`pg_hba.conf`**
  #### Windows
  
   - Método 1 - Via linha de comando do PostgreSQL
   ```
   psql -U postgres -c "SHOW hba_file;
   ```
   - Método 2 - Buscar no explorador de arquivos
   ```
   C:\Program Files\PostgreSQL\<versão>\data\pg_hba.conf
   ```
  - Método 3 - Buscar com PowerShell
  ```
  Get-ChildItem -Path C:\ -Name pg_hba.conf -Recurse -ErrorAction SilentlyContinue
  ```
  #### Linux
   - Método 1 - Via linha de comando do PostgreSQL
   ```
   sudo -u postgres psql -c "SHOW hba_file;"
   ```
   - Método 2 - Locais comuns
   ```
   /etc/postgresql/<versão>/main/pg_hba.conf
   /var/lib/pgsql/data/pg_hba.conf
   /var/lib/postgresql/<versão>/main/pg_hba.conf
   ```
  - Método 3 - Buscar em todo o sistema
  ```
  sudo find / -name pg_hba.conf 2>/dev/null
  ```
  #### macOS(Homebrew)
  - Método 1 - Comando do PostgreSQL
   ```
   psql -c "SHOW hba_file;"
   ```
   - Método 2 - Locais comuns do Homebrew
   ```
   /usr/local/var/postgres/pg_hba.conf
   /opt/homebrew/var/postgres/pg_hba.conf
   ```
  - Método 3 -Buscar no sistema
  ```
  sudo find / -name pg_hba.conf 2>/dev/null | grep -v Permission
  ```
2. Edite o arquivo pg_hba.conf
 #### Windows
   - Método 1 - Bloco de Notas como administrador
    ```
   notepad "C:\Program Files\PostgreSQL\15\data\pg_hba.conf"
    ```

   - Método 2 - PowerShell com Notepad++
    ```
   notepad++ "C:\Program Files\PostgreSQL\15\data\pg_hba.conf"
    ```
   - Método 3 - VS Code (como administrador)
    ```
   code "C:\Program Files\PostgreSQL\15\data\pg_hba.conf"
    ```
#### Linux
   - Método 1 - Nano (sudo necessário)
   ```
   sudo nano /etc/postgresql/15/main/pg_hba.conf
   ```
   - Método 2 - Vim
   ```
   sudo vim /etc/postgresql/15/main/pg_hba.conf
   ```
   - Método 3 - Gedit (interface gráfica)
   ```
   sudo gedit /etc/postgresql/15/main/pg_hba.conf
   ```
   - Método 4 - VS Code
   ```
   code /etc/postgresql/15/main/pg_hba.conf
   ```
   - Método 5 - Visualizar sem editar
   ```
   sudo cat /etc/postgresql/15/main/pg_hba.conf
   ```
#### macOS(Homebrew)
   - Método 1 - Nano
   ```
   sudo nano /usr/local/var/postgres/pg_hba.conf
   ```
   - Método 2 - Vim
   ```
   sudo vim /usr/local/var/postgres/pg_hba.conf
   ```
   - Método 3 - TextEdit (via comando)
   ```
   open -a TextEdit /usr/local/var/postgres/pg_hba.conf
   ```
   - Método 4 - VS Code
   ```
   code /usr/local/var/postgres/pg_hba.conf
   ```
Para **acesso local seguro**, recomenda-se a configuração:
```
# Tipo  Banco  Usuário  Endereço  Método
local   all     all               md5
```
- **local** → acesso apenas do computador local.
- **all** → aplica para todos os bancos e todos os usuários.
- **md5** → exige senha criptografada.

Depois de alterar, **é preciso reiniciar o serviço** para aplicar as mudanças.

### 💻 Windows

1. O PostgreSQL já cria um usuário administrador chamado `postgres`.  
2. Durante a instalação, você já **definiu a senha do `postgres`**.  

## 🐧 Linux (Ubuntu/Debian)

1. O PostgreSQL cria o usuário do sistema `postgres`.  
2. Para definir uma senha do administrador:
```bash
sudo -i -u postgres
psql
\password postgres
```
###🍎 macOS

1. Por padrão, o usuário administrador é o mesmo do sistema e pode acessar sem senha.
2. Para criar um acesso seguro, crie um usuário com senha:
```bash
   psql
CREATE USER meu_usuario WITH PASSWORD 'minha_senha';
```
#### baasb
---

## Criar banco de dados e usuário para o projeto
