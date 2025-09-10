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

### 🔐 Configuração da Senha

| Sistema Operacional | Usuário Padrão | Configuração de Senha | Comandos |
|---------------------|----------------|------------------------|----------|
| **🪟 Windows** | `postgres` | Definida durante a instalação | *Senha configurada no processo de instalação* |
| **🐧 Linux** | `postgres` (usuário do sistema) | Deve ser definida manualmente | ```sudo -i -u postgres psql \password postgres``` |
| **🍎 macOS** | Mesmo usuário do sistema | Acesso sem senha por padrão | ```psql CREATE USER meu_usuario WITH PASSWORD 'minha_senha';``` |

---
