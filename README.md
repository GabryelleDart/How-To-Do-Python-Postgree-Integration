# 🐍💾 How-To-Do-Python-PostgreSQL-Integration

<intro>

---

## 📖 Sobre o Projeto
Este repositório tem como objetivo ajudar você a:  
✅ Entender o que é o **PostgreSQL**  
✅ Aprender como **instalar e configurar** o banco de dados em diferentes sistemas operacionais  
✅ Criar um **banco de dados seguro**, com usuário próprio para cada aplicação  
✅ Definir **entidades e atributos** de um sistema real (exemplo: gestão de saúde)  
✅ Modelar **relacionamentos entre tabelas** no PostgreSQL  
✅ Construir o **esquema do banco de dados** de forma organizada  
✅ Integrar o **Python com PostgreSQL** utilizando bibliotecas como `psycopg2`  

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
   - 📖 **Documentação teórica** → explicações sobre PostgreSQL, instalação e conceitos          básicos.  
   - 🗂️ **Scripts SQL** → arquivos prontos para criar usuários, bancos e esquemas no             PostgreSQL.  
   - 🐍 **Exemplos em Python** → conexão com PostgreSQL, execução de queries e boas práticas. 
   - 📊 **Modelagem de dados** → entidades, atributos e relacionamentos representados em SQL      e diagramas.  
   - 🔐 **Configurações de segurança** → como proteger seu banco com acesso local seguro.  
   - 📁 **Exemplos práticos** → simulação de um sistema de saúde para aplicar todos os            conceitos.  

> 💡 Assim, o repositório serve tanto como **material de estudo** quanto como **base inicial** para novos projetos que integrem Python + PostgreSQL.  

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
- Iniciar: sudo systemctl start postgresql

- Parar: sudo systemctl stop postgresql

- Reiniciar: sudo systemctl restart postgresql

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





&nbsp;<br>
&nbsp;<br>
&nbsp;<br>
&nbsp;<br>
&nbsp;<br>
&nbsp;<br>









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
  #### 💻 Windows
  
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
  #### 🐧 Linux
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
  #### 🍎 macOS(Homebrew)
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
 #### 💻 Windows
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
#### 🐧 Linux
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
#### 🍎 macOS(Homebrew)
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






&nbsp;<br>
&nbsp;<br>
&nbsp;<br>
&nbsp;<br>
&nbsp;<br>
&nbsp;<br>






## 🗃️ Criar banco de dados e usuário para o projeto

### 🔎 O que é isso e por que é importante?
- **Banco de dados**: é o lugar onde sua aplicação guarda informações, como uma super planilha inteligente.  
- **Usuário**: é a conta que acessa o banco.  
- **Por que criar um usuário separado para o projeto?**
  - Segurança: não use a conta de administrador (`postgres`) no dia a dia.  
  - Organização: cada projeto com seu banco e usuário.  
  - Controle: você decide quem pode ver ou mudar dados.
 
### 💻 Métodos de criar banco e usuário

Você pode fazer isso de várias formas, dependendo do seu sistema ou preferência: **linha de comando, script SQL, GUI, Docker**.
```
Obs: Docker não será abordado nesse README pois não fez parte do escopo de estudo da Sprint, mas deixamos como informação adicional para possiveis pesquisas futuras.
```
#### 1️⃣ Linha de comando (`psql`) — Windows, Linux e macOS

**Passo 1:** Conectar como administrador  

- **Windows**:
```bash
psql -U postgres -h localhost -W
```
- **Linux**:
```bash
sudo -i -u postgres
psql
```
- **macOS**:
```bash
psql
```
**Passo 2:** Criar usuário e senha
```bash
CREATE USER meu_usuario WITH PASSWORD 'minha_senha_segura';
```
**Passo 3:** Criar banco e definir o dono
```bash
CREATE DATABASE meu_projeto OWNER meu_usuario;
```
**Passo 4:** Dar permissões básicas
```bash
GRANT ALL PRIVILEGES ON DATABASE meu_projeto TO meu_usuario;
```
> OBS: Você pode conceder só as permissões que o usuário precisa.
> 
#### 2️⃣ Usando script SQL (arquivo .sql)

**Passo 1:**  Crie um arquivo chamado setup.sql:
```bash
CREATE USER meu_usuario WITH PASSWORD 'minha_senha_segura';
CREATE DATABASE meu_projeto OWNER meu_usuario;
GRANT ALL PRIVILEGES ON DATABASE meu_projeto TO meu_usuario;
```
**Passo 1:** Execute o script:
| Sistema Operacional | Comando |
|---------------------|---------|
| Linux | `sudo -u postgres psql -f setup.sql` |
| Windows/macOS | `psql -U postgres -f setup.sql` |

#### 3️⃣ Usando GUI (Interface Gráfica)/
> Nessa explicação será demonstrado com **pgAdmin**, a interface gráfica do Postgre.

**Passo 1:**  Abra a ferramenta e conecte-se como postgres.
   
<img width="1919" height="1020" alt="Captura de tela 2025-09-11 152753" src="https://github.com/user-attachments/assets/edfdc68f-8bef-40fb-88f3-7a0ef0e75859" />

**Passo 2:** Crie um usuário com senha (Login/Role) e ajuste permissões conforme necessário.
   
<img width="1919" height="1018" alt="Captura de tela 2025-09-11 152809" src="https://github.com/user-attachments/assets/608ae725-3190-41d7-8f2e-4f369c48ebc4" />

<img width="1919" height="1010" alt="Captura de tela 2025-09-11 152855" src="https://github.com/user-attachments/assets/ff8a383f-a18b-4711-95a6-8ff834a9ea82" />

<img width="1919" height="1014" alt="Captura de tela 2025-09-11 153207" src="https://github.com/user-attachments/assets/c6f9c80c-c8ff-47bd-91af-59c57209de27" />

> Ao não preencher o **Account expires** a conta da *maria* não terá uma data de validade.
> Ao deixar **Connection limit** em -1 , estou dizendo ao sistema que a conta não terá limite de conexão.

<img width="1919" height="1016" alt="Captura de tela 2025-09-11 153230" src="https://github.com/user-attachments/assets/2332ad04-7746-4488-98fb-10b2bae56ecf" />

**Passo 3:**  Crie um banco de dados e defina esse usuário como dono.
<img width="1910" height="963" alt="Captura de tela 2025-09-11 153737" src="https://github.com/user-attachments/assets/b2695837-e76d-43e2-9f90-7bb639e14653" />

<img width="1919" height="544" alt="image" src="https://github.com/user-attachments/assets/6391d476-2f5f-48ea-8950-700f81247fe7" />

<img width="1919" height="1011" alt="image" src="https://github.com/user-attachments/assets/d45e250f-60cf-4d47-a40a-6feb3dc0a427" />

<img width="1915" height="1002" alt="image" src="https://github.com/user-attachments/assets/192a612d-8526-4204-8819-21b8d77b4fa3" />

**Passo 4:** Salve.

---


&nbsp;<br>
&nbsp;<br>
&nbsp;<br>
&nbsp;<br>
&nbsp;<br>
&nbsp;<br>









## 📐 Definir Entidades e Atributos do Banco de Dados

### 🔎 O que são **entidades**?

- **Entidades** são os "objetos" ou "coisas" que queremos representar no banco de dados.  
- Podem ser **pessoas, lugares, objetos, eventos ou conceitos** relevantes para o projeto.
  
### 👨‍⚕️ Exemplo prático para Sistema de Saúde:
Em um sistema de gestão hospitalar, algumas entidades podem ser:
- Paciente
- Médico
- Consulta
- Prontuário
- Exame
- Medicamento
### 🔑 O que são **atributos**?

- **Atributos** são as **características** ou **informações** de cada entidade.  
- Eles funcionam como colunas de uma tabela. 
> **👨‍⚕️Exemplo no Contexto de Saúde:** Se a entidade é Paciente, seus atributos podem ser nome, data_nascimento, CPF, CNS, telefone, tipo_sanguineo.

### 🧩 Modelagem de Banco de Dados: Conceitual, Lógico e Físico

Antes de criar as entidades e atributos no PostgreSQL, precisamos entender **como planejar o banco de dados**.  
Esse planejamento é feito em **três níveis de modelagem**:
#### 1️⃣ Modelo Conceitual
- **O que é**: visão mais **abstrata**, mostrando **quais entidades existem** e como se relacionam.
- **Ferramenta típica**: diagrama ER (Entidade-Relacionamento).

📌 **Exemplo:**
- Entidades :
  - **Cidadão** (dados demográficos, endereço, contato)
  - **Equipe de Saúde** (equipe responsável pelo cidadão)
  - **Raça/Cor** (classificação demográfica)
  - **Sexo** (cadastro do sexo do cidadão)
  - **Medição** (peso, altura, pressão, IMC, etc.)
  - **Exame** (colesterol total, outros exames)
  - **Evolução/Objetivo de Atendimento**
 
 - Relações:
  - Um **Cidadão** é **vinculado** a uma **Equipe de Saúde**.  
  - Um **Cidadão** possui um registro de **Sexo** e **Raça/Cor**.  
  - Um **Cidadão** pode ter **diversas medições** ao longo do tempo.  
  - Um **Cidadão** pode ter **exames laboratoriais** (ex.: colesterol).  
  - Um **Atendimento** gera uma **Evolução/Objetivo** registrado pelo profissional.

> 👉 O modelo conceitual é para **entender o que existe** no sistema, sem pensar ainda em tabelas ou SQL.

#### 2️⃣ Modelo Lógico

- **O que é**: tradução do conceitual para tabelas e atributos, mas ainda sem detalhes técnicos de PostgreSQL.  
- **Objetivo**: organizar **entidades, atributos, chaves primárias e estrangeiras**.
  
📌 Representação lógica:
<img width="828" height="498" alt="diagrama lógico pet saúde" src="https://github.com/user-attachments/assets/542f7d3f-42f0-410f-8792-6475f61eccee" />

>👉 O modelo lógico mostra **como os dados se conectam**, mas ainda não escolhemos detalhes técnicos do PostgreSQL.

#### 3️⃣ Modelo Físico
- **O que é**: é a versão **implementável** no banco real (PostgreSQL).  
- **Objetivo**: definir **tipos de dados, constraints, índices, chaves**.

>👉 O modelo físico é o que o PostgreSQL entende e executa.

### 💻 Como definir entidades e atributos no PostgreSQL
Existem várias formas de criar isso no PostgreSQL.  
#### 1️⃣ Usando SQL direto (CREATE TABLE)
```sql
-- Tabela de tipos de unidade (dimensão)
CREATE TABLE dim_tipo_unidade (
    co_seq_tipo_unidade BIGSERIAL PRIMARY KEY,   -- Identificador único
    ds_tipo_unidade VARCHAR(100) UNIQUE NOT NULL -- Nome do tipo da unidade (ex: Hospital, UBS)
);

-- Tabela de sexos (dimensão)
CREATE TABLE dim_sexo (
    co_seq_sexo BIGSERIAL PRIMARY KEY,   -- Identificador único
    ds_sexo VARCHAR(50) UNIQUE NOT NULL, -- Masculino, Feminino, Outro
    sg_sexo CHAR(1)                      -- Sigla (M, F, O)
);

-- Tabela de unidades de saúde
CREATE TABLE tb_unidade_saude (
    co_seq_unidade_saude BIGSERIAL PRIMARY KEY,
    no_unidade VARCHAR(255) NOT NULL,   -- Nome da unidade
    ds_endereco TEXT,                   -- Endereço completo
    nu_cnes VARCHAR(20) UNIQUE,         -- Código CNES da unidade
    co_tipo_unidade BIGINT NOT NULL,    -- Relaciona com a tabela de tipos de unidade

    CONSTRAINT fk_tipo_unidade
        FOREIGN KEY(co_tipo_unidade) 
        REFERENCES dim_tipo_unidade(co_seq_tipo_unidade) -- Chave estrangeira
);

-- Tabela de pacientes
CREATE TABLE tb_paciente (
    co_seq_paciente BIGSERIAL PRIMARY KEY,
    no_paciente VARCHAR(255) NOT NULL,      -- Nome completo
    no_social_paciente VARCHAR(255),        -- Nome social
    dt_nascimento DATE NOT NULL,            -- Data de nascimento
    nu_cpf VARCHAR(11) UNIQUE NOT NULL,     -- CPF
    nu_cns VARCHAR(16) UNIQUE,              -- Cartão SUS
    co_sexo BIGINT,                         -- Relaciona com a tabela de sexo
    
    CONSTRAINT fk_sexo
        FOREIGN KEY(co_sexo) 
        REFERENCES dim_sexo(co_seq_sexo)
);

-- Tabela de atendimentos
CREATE TABLE tb_atendimento (
    co_seq_atendimento BIGSERIAL PRIMARY KEY,
    dt_atendimento TIMESTAMP WITH TIME ZONE DEFAULT now(), -- Data e hora do atendimento
    ds_resumo_atendimento TEXT,                            -- Resumo da consulta
    co_paciente BIGINT NOT NULL,                           -- Relaciona com paciente
    co_unidade_saude BIGINT NOT NULL,                      -- Relaciona com unidade de saúde

    -- Relaciona com paciente (se o paciente for deletado, seus atendimentos também serão)
    CONSTRAINT fk_paciente
        FOREIGN KEY(co_paciente) 
        REFERENCES tb_paciente(co_seq_paciente) ON DELETE CASCADE,

    -- Relaciona com unidade de saúde (mesma lógica do paciente)
    CONSTRAINT fk_unidade_saude
        FOREIGN KEY(co_unidade_saude) 
        REFERENCES tb_unidade_saude(co_seq_unidade_saude) ON DELETE CASCADE
);
````
>👉 Cada CREATE TABLE cria uma entidade (tabela).
>👉 Cada linha dentro da tabela define um atributo (coluna).
>👉 As chaves estrangeiras (FOREIGN KEY) criam relações entre as entidades.

> ‼️ Caso houver estranhamento acerca das nomeclaturas utilizadas, acesse o documento :[📊Significado dos campos das tabelas indicadas .pdf]([./caminho/do/arquivo.pdf](https://github.com/GabryelleDart/How-To-Do-Python-Postgree-Integration/blob/main/Significado%20dos%20campos%20das%20tabelas%20indicadas%20.pdf))
#### 2️⃣ Usando pgAdmin (interface gráfica)
   1. Abra o pgAdmin.
   2. Clique em Databases → Seu banco → Schemas → Tables.
   3. Clique com o botão direito → Create → Table.
<img width="1919" height="1016" alt="Captura de tela 2025-09-11 172908" src="https://github.com/user-attachments/assets/69614482-754b-4a86-9b4b-aea3e2c62707" />
   4. Defina o nome da entidade (ex: tb_paciente).
<img width="1919" height="1006" alt="Captura de tela 2025-09-11 173226" src="https://github.com/user-attachments/assets/bf53a0a9-444d-4f76-9236-b6e6e9b8f43b" />
   5. Em Columns, adicione os atributos (colunas, tipo de dado, se é obrigatório, se é chave primária).
<img width="1919" height="997" alt="Captura de tela 2025-09-11 173357" src="https://github.com/user-attachments/assets/12cc2522-09e7-4250-8656-4636ee071a3e" />
   6. Salve.

> Método ideal para quem prefere clicar em menus em vez de digitar comandos.
> 
#### 3️⃣ Usando Scripts SQL (para rodar várias vezes)
   1. Crie um arquivo chamado `schema.sql`.
   2. Cole dentro dele o mesmo código mostrado em  `Usando SQL direto (CREATE TABLE)`.
   3. Execute o script no terminal:

   | Sistema Operacional | Comando |
   |---------------------|---------|
   | Linux/macOS | `psql -U meu_usuario -d meu_projeto -f schema.sql` |
   | Windows | `psql -U meu_usuario -d meu_projeto -f "C:\caminho\para\schema.sql"` |
---


&nbsp;<br>
&nbsp;<br>
&nbsp;<br>
&nbsp;<br>
&nbsp;<br>
&nbsp;<br>








## 🗂️ Modelar Relações entre as Tabelas no PostgreSQL

### 📖 O que significa modelar relações?
Modelar relações é definir como tabelas diferentes de um banco de dados se conectam.
➡️ No mundo real:
- Um paciente pode ter vários atendimentos.
- Um hospital pode atender vários pacientes.
- Cada atendimento está ligado a um paciente e a um hospital.

No banco de dados, essas conexões são chamadas de relacionamentos.

### 🧩 Tipos de Relacionamentos
| Tipo | Entidade 1 | Cardinalidade | Entidade 2 | Exemplo |
|------|------------|---------------|------------|---------|
| **1:1** | `paciente` | `1` ─── `1` | `documento` | Um paciente tem um único CPF |
| **1:N** | `dim_tipo_unidade` | `1` ─── `N` | `tb_unidade_saude` | Um tipo tem várias unidades |
| **1:N** | `dim_sexo` | `1` ─── `N` | `tb_paciente` | Um sexo tem vários pacientes |
| **1:N** | `tb_paciente` | `1` ─── `N` | `tb_atendimento` | Um paciente tem vários atendimentos |
| **1:N** | `tb_unidade_saude` | `1` ─── `N` | `tb_atendimento` | Uma unidade tem vários atendimentos |
| **N:N** | `tb_paciente` | `N` ─── `N` | `tb_medico` | Pacientes ↔ Médicos |

### 📊 Métodos para modelar relações
Existem várias formas de criar relações entre tabelas no PostgreSQL. Vamos ver todas:
#### 🔹 1. Via SQL (padrão e mais usado)

O jeito mais direto é escrever os comandos SQL que criam as chaves estrangeiras (FOREIGN KEYS).
Exemplo:
```sql
-- Criar tabela de tipos de unidade
CREATE TABLE dim_tipo_unidade (
    co_seq_tipo_unidade BIGSERIAL PRIMARY KEY,
    ds_tipo_unidade VARCHAR(100) UNIQUE NOT NULL
);

-- Criar tabela de unidades de saúde e ligar ao tipo
CREATE TABLE tb_unidade_saude (
    co_seq_unidade_saude BIGSERIAL PRIMARY KEY,
    no_unidade VARCHAR(255) NOT NULL,
    co_tipo_unidade BIGINT NOT NULL,

    CONSTRAINT fk_tipo_unidade
        FOREIGN KEY(co_tipo_unidade) 
        REFERENCES dim_tipo_unidade(co_seq_tipo_unidade)
);
```
> 👉 Aqui, a relação é 1 tipo de unidade → várias unidades de saúde (1:N).
** 📌 Vantagem: mais flexível, você escreve exatamente o que precisa.**
** 📌 Desvantagem: precisa conhecer SQL.**

#### 🔹 2. Usando pgAdmin (Interface Gráfica)

1. Abra o pgAdmin e conecte ao seu banco de dados.

2. No painel lateral, vá até Schemas → Tables.

3. Clique com o botão direito na tabela que vai receber a chave estrangeira (ex.: tb_unidade_saude).

<img width="1919" height="1016" alt="Captura de tela 2025-09-11 220240" src="https://github.com/user-attachments/assets/464e60f1-9b30-4082-ab98-03d01520cb30" />

4. Selecione Properties → Constraints → Foreign Keys.

5. Clique em + para adicionar uma nova foreign key.

6. Configure:
   
- Nome da constraint (ex.: fk_tipo_unidade)
  
- Coluna da tabela atual (ex.: co_tipo_unidade)
  
- Tabela de referência (ex.: dim_tipo_unidade)
  
- Coluna de referência (ex.: co_seq_tipo_unidade)
  
<img width="1919" height="1010" alt="image" src="https://github.com/user-attachments/assets/352950a1-9037-4163-b1a2-785719abd51d" />

7. Clique em Save.

**📌 O pgAdmin vai gerar automaticamente o comando SQL equivalente.**

#### 🔹 3. Usando Diagramas ERD no pgAdmin

O pgAdmin tem uma ferramenta chamada ERD Tool (Entity-Relationship Diagram), que permite criar relações arrastando e soltando.

Como usar:

1. Abra o pgAdmin.
2. Vá em Tools → ERD Tool.
3. Adicione as tabelas que já existem no banco.
4. Clique em uma coluna e arraste até a coluna da tabela relacionada.
> O pgAdmin gera o relacionamento visualmente e o SQL correspondente.
5. Clique em Generate SQL → Run para aplicar no banco.

📌 Vantagem: Muito bom para quem prefere trabalhar visualmente.

📌 Desvantagem: Menos controle fino do que escrever SQL diretamente.

----


&nbsp;<br>
&nbsp;<br>
&nbsp;<br>
&nbsp;<br>
&nbsp;<br>
&nbsp;<br>








## 🗂️ Criar o esquema do Banco de Dados

### 📖 O que é um esquema?
Um esquema no PostgreSQL é como uma pasta dentro do banco de dados.
- Ele organiza tabelas, visões, funções e outros objetos.
- Permite separar diferentes partes de um sistema dentro do mesmo banco.

➡️ Por padrão, o PostgreSQL cria o esquema chamado `public`, onde tudo é armazenado.
➡️ Mas, em projetos reais, é comum criar esquemas separados (ex.: `clinica`, `financeiro`, `usuarios`) para organizar melhor.

🎯 Por que usar esquemas?

- Organização → Evita confusão em projetos grandes.
- Segurança → Permite dar permissões diferentes por esquema.
- Reuso → Dá para ter tabelas com o mesmo nome em esquemas diferentes.

> **👉 OBSERVAÇÃO:** Se você não especificar um esquema, o PostgreSQL usa automaticamente o `public`.
Exemplo: 
- `clinica.tb_paciente`
- `financeiro.tb_paciente`
> Mesmo nome, mas em contextos diferentes.

### 📖 Como criar esquemas no PostgreSQL

#### 🔹 1. Criar esquema via SQL
O comando básico é:
```sql
CREATE SCHEMA nome_do_esquema;
```
Exemplo:
```sql
CREATE SCHEMA clinica;
```
Logo, todas as tabelas da clínica podem ser criadas assim:
```sql
CREATE TABLE clinica.tb_paciente (
    id BIGSERIAL PRIMARY KEY,
    nome VARCHAR(255) NOT NULL
);
```
> 🍭 É possível definir qual esquema será usado por padrão quando o usuário logar. Por meio do código `ALTER USER meu_usuario SET search_path TO clinica;`

##### 👁️ Como ver esquemas existentes?
Execute dentro do psql:
```sql
\dn
```
### 🔹 2. Criar esquema via pgAdmin
1. Abra o pgAdmin.
2. No painel lateral, expanda o banco de dados.
3. Clique em Schemas → Create → Schema.
<img width="1919" height="1013" alt="Captura de tela 2025-09-11 212554" src="https://github.com/user-attachments/assets/9ab71a67-a725-48d6-b0ac-c008c9040bfb" />
4. Dê um nome (ex.: clinica).
<img width="1919" height="1014" alt="image" src="https://github.com/user-attachments/assets/329ba02a-5efb-4a15-8c4f-2353a6b12102" />
5. Clique em Save.

&nbsp;<br>
&nbsp;<br>
&nbsp;<br>
&nbsp;<br>
&nbsp;<br>
&nbsp;<br>








## 🚀 Escrever e Executar Queries (Consultas) no Banco de Dados

Com nosso banco de dados, tabelas e usuários devidamente estruturados, o próximo passo é interagir com os dados. Esta seção cobre as operações essenciais de um banco de dados: Inserir, Atualizar, Remover e, o mais importante, Consultar informações.

### 📝 O que são Queries SQL?

**Queries** (ou consultas) são os comandos que enviamos para o banco de dados para que ele execute uma ação. Elas são escritas em uma linguagem chamada **SQL** (Structured Query Language). As operações básicas são divididas em duas categorias principais:

  - **DML (Data Manipulation Language):** Comandos que manipulam os dados.
      - `INSERT`: Adiciona novos registros.
      - `UPDATE`: Modifica registros existentes.
      - `DELETE`: Remove registros existentes.
  - **DQL (Data Query Language):** Comandos que consultam os dados.
      - `SELECT`: Extrai e lê informações das tabelas.

-----

### 🛠️ Passo a Passo: Manipulando e Consultando Dados

As queries a seguir devem ser executadas em uma ferramenta de banco de dados como **DBeaver** ou **pgAdmin**, conectado ao banco `petsaude_vca` com o usuário `petsaude_user`.

#### 🔵 Inserção, Atualização e Remoção (DML)

##### 1\. Inserção de Dados (`INSERT`)

Primeiro, vamos povoar nossas tabelas com dados de exemplo para que possamos trabalhar. A ordem é importante: primeiro inserimos os dados nas tabelas de "dimensão" (`dim_`) e depois nas tabelas principais (`tb_`) que dependem delas.

```sql
-- PASSO 1: Povoar as tabelas de dimensão PRIMEIRO.
INSERT INTO dim_tipo_unidade (ds_tipo_unidade) VALUES 
('Unidade Básica de Saúde'), 
('Hospital'), 
('Centro de Atenção Psicocial (CAPS)');

INSERT INTO dim_sexo (ds_sexo, sg_sexo) VALUES 
('Feminino', 'F'), 
('Masculino', 'M'),
('Não Declarado', 'N');

-- PASSO 2: Povoar as tabelas principais.
INSERT INTO tb_unidade_saude (no_unidade, ds_endereco, nu_cnes, co_tipo_unidade) VALUES
('UBS Dr. Régis Pacheco', 'Praça Sá Barreto, s/n - Centro', '2334567', 1),
('Hospital Geral de Vitória da Conquista (HGVC)', 'Av. Filipinas, s/n - Candeias', '5543210', 2),
('CAPS II Arnaldo de Carvalho', 'Av. Presidente Vargas, 123 - Jurema', '8876543', 3);

INSERT INTO tb_paciente (no_paciente, no_social_paciente, dt_nascimento, nu_cpf, nu_cns, co_sexo) VALUES
[cite_start]('Ana Clara Guimarães', NULL, '1995-03-15', '11122233301', '89800101234acabou de ser atualizado. [cite: 1]
('Bruno Oliveira Santos', NULL, '1988-11-20', '44455566602', '898002098765432', 2),
('Carla Dias de Jesus', 'Carlos Dias de Jesus', '2001-07-02', '77788899903', '898003011223344', 1),
('Davi Souza Lima', NULL, '1954-01-30', '10120230304', '898004055667788', 2);

-- PASSO 3: Povoar a tabela de atendimentos, conectando pacientes e unidades.
INSERT INTO tb_atendimento (co_paciente, co_unidade_saude, ds_resumo_atendimento) VALUES
(1, 1, 'Consulta de rotina. Paciente relata bom estado de saúde geral. Aferida pressão arterial: 120/80 mmHg.'),
(2, 2, 'Entrada no pronto-socorro com dores abdominais agudas. Suspeita de apendicite. Encaminhado para exames.'),
(1, 1, 'Retorno para mostrar exames. Resultados normais. Aconselhada a manter dieta equilibrada.'),
(4, 3, 'Sessão de terapia em grupo. Paciente idoso participativo e comunicativo.'),
(3, 1, 'Acolhimento e atualização de cadastro. Paciente solicitou informações sobre programa de saúde da mulher.');
```

##### 2\. Atualização de Dados (`UPDATE`)

O comando `UPDATE` é usado para modificar um registro que já existe. Por exemplo, vamos corrigir o endereço do paciente Bruno Oliveira Santos.

```sql
UPDATE tb_paciente
SET ds_endereco = 'Avenida Olívia Flores, 1500 - Candeias'
WHERE nu_cpf = '44455566602';
```

> ⚠️ **MUITO IMPORTANTE:** Use sempre a cláusula `WHERE` em um `UPDATE`. Se você esquecer, **TODOS** os registros da tabela serão atualizados\!

##### 3\. Remoção de Dados (`DELETE`)

O comando `DELETE` é usado para apagar registros. Vamos supor que o atendimento do paciente Davi Souza Lima foi registrado por engano.

```sql
DELETE FROM tb_atendimento
WHERE co_paciente = 4; -- Assumindo que o ID do Davi é 4
```

> ⚠️ **CUIDADO:** Assim como no `UPDATE`, a cláusula `WHERE` é fundamental. Sem ela, você apagará **TODOS** os dados da tabela\!

-----

#### 🔵 Escrita de Queries de Consulta (DQL)

Agora que temos dados, podemos fazer perguntas ao nosso banco de dados. Para isso, usamos o comando `SELECT`, que é a base para toda extração de informações.

##### 📈 Consulta 1: Listar Todos os Pacientes

Vamos começar com a consulta mais simples para ver todos os pacientes cadastrados, ordenando o resultado por nome.

  - `SELECT *`: É o comando que diz "selecione todas as colunas".
  - `FROM tb_paciente`: Especifica de qual tabela queremos buscar os dados, neste caso, a `tb_paciente`.
  - `ORDER BY no_paciente`: É opcional e serve para ordenar os resultados. Aqui, estamos ordenando alfabeticamente pela coluna `no_paciente`.

<!-- end list -->

```sql
SELECT * FROM tb_paciente
ORDER BY no_paciente;
```

##### 👤 Consulta 2: Encontrar um Paciente Específico

Para buscar apenas os dados de um paciente a partir do seu CPF, adicionamos um filtro.

  - `WHERE nu_cpf = '11122233301'`: A cláusula `WHERE` é o nosso filtro. Ela diz ao banco para retornar apenas as linhas que satisfazem uma condição específica.

<!-- end list -->

```sql
SELECT * FROM tb_paciente 
WHERE nu_cpf = '11122233301';
```

##### 📄 Consulta 3: Relatório Completo de Atendimentos

Esta é a consulta mais poderosa, pois ela combina informações de várias tabelas para criar um relatório que faz sentido para um ser humano.

  - `JOIN`: É o comando que "conecta" as tabelas. Ele combina linhas de uma tabela com as linhas de outra com base em uma coluna relacionada.
  - `AS`: É um "apelido" (`alias`). Usamos `tb_atendimento AS a` para poder nos referir à tabela `tb_atendimento` usando apenas a letra `a`, o que torna a query mais curta e legível.
  - `ON`: Usado sempre com o `JOIN`, ele especifica a "regra da conexão". `ON a.co_paciente = p.co_seq_paciente` diz ao banco para conectar as linhas onde o ID do paciente na tabela de atendimentos é igual ao ID na tabela de pacientes.

<!-- end list -->

```sql
SELECT
    a.dt_atendimento,
    p.no_paciente,
    p.dt_nascimento,
    s.ds_sexo,
    u.no_unidade,
    tu.ds_tipo_unidade,
    a.ds_resumo_atendimento
FROM
    tb_atendimento AS a
JOIN
    tb_paciente AS p ON a.co_paciente = p.co_seq_paciente
JOIN
    tb_unidade_saude AS u ON a.co_unidade_saude = u.co_seq_unidade_saude
JOIN
    dim_sexo AS s ON p.co_sexo = s.co_seq_sexo
JOIN
    dim_tipo_unidade AS tu ON u.co_tipo_unidade = tu.co_seq_tipo_unidade
ORDER BY
    a.dt_atendimento DESC; -- Ordena pelos mais recentes primeiro
```

##### 🏥 Consulta 4: Contar Atendimentos por Unidade

Às vezes, não queremos ver os dados brutos, mas sim um resumo, um totalizador.

  - `COUNT(a.co_seq_atendimento)`: `COUNT` é uma **função de agregação**. Ela conta o número de linhas. Aqui, estamos contando quantos atendimentos existem.
  - `GROUP BY u.no_unidade`: A cláusula `GROUP BY` agrupa todas as linhas que têm o mesmo valor na coluna `no_unidade` em uma única linha de resumo, permitindo que o `COUNT` funcione para cada grupo separadamente.

<!-- end list -->

```sql
SELECT
    u.no_unidade,
    count(a.co_seq_atendimento) AS total_de_atendimentos
FROM
    tb_atendimento AS a
JOIN
    tb_unidade_saude AS u ON a.co_unidade_saude = u.co_seq_unidade_saude
GROUP BY
    u.no_unidade
ORDER BY
    total_de_atendimentos DESC;
```

##### 🧑‍⚕️ Consulta 5: Listar Atendimentos de um Paciente Específico

Agora, vamos combinar `JOIN` e `WHERE` para ver todo o histórico de atendimentos da paciente "Ana Clara Guimarães".

```sql
SELECT
    a.dt_atendimento,
    u.no_unidade,
    a.ds_resumo_atendimento
FROM
    tb_atendimento AS a
JOIN
    tb_paciente AS p ON a.co_paciente = p.co_seq_paciente
JOIN
    tb_unidade_saude AS u ON a.co_unidade_saude = u.co_seq_unidade_saude
WHERE
    p.no_paciente = 'Ana Clara Guimarães'
ORDER BY
    a.dt_atendimento;
```


&nbsp;<br>
&nbsp;<br>
&nbsp;<br>
&nbsp;<br>
&nbsp;<br>
&nbsp;<br>








## 🔗 Conectar Python ao PostgreSQL e Executar Consultas

Esta seção é o guia definitivo para a etapa final do nosso projeto: fazer a aplicação Python se conectar ao banco de dados, executar uma consulta real com `JOIN`s e exibir um relatório formatado.

-----

### 📝 Pré-requisitos Essenciais

Antes de tocar em qualquer código Python, verifique se os seguintes pontos estão 100% corretos. A maioria dos erros acontece por problemas na base.

  - ✅ **Servidor PostgreSQL Rodando:** Garanta que o serviço do PostgreSQL foi iniciado no seu computador.
  - ✅ **Banco e Usuário Criados:** Você precisa ter executado os passos da seção anterior, criando o banco `petsaude_vca` e o usuário `petsaude_user`.
  - ✅ **Permissões do Usuário Concedidas:** Este é um passo crítico. O usuário `petsaude_user` não tem permissão para nada por padrão. **Conecte-se como `postgres`** e execute o script abaixo para evitar o erro de `permissão negada`.

<!-- end list -->

```sql
-- SCRIPT DE PERMISSÕES (Execute no DBeaver/pgAdmin como 'postgres')

-- 1. Permite que o usuário acesse o esquema 'public'
GRANT USAGE ON SCHEMA public TO petsaude_user;

-- 2. Permite que o usuário leia TODAS as tabelas no esquema 'public'
GRANT SELECT ON ALL TABLES IN SCHEMA public TO petsaude_user;

-- 3. Permite que o usuário escreva (INSERT, UPDATE, DELETE) nas tabelas de dados
GRANT INSERT, UPDATE, DELETE ON tb_atendimento, tb_paciente, tb_unidade_saude TO petsaude_user;

-- 4. Permite que o usuário use as sequências de ID automático (essencial para INSERTs)
GRANT USAGE, SELECT ON ALL SEQUENCES IN SCHEMA public TO petsaude_user;
```

-----

### ⚙️ Passo 1: Configurando o Ambiente Python

Agora, vamos preparar a "sala" onde nosso código Python vai rodar.

1.  **Crie e Ative um Ambiente Virtual (`venv`)**
    Isso cria uma instalação Python isolada para o projeto. No terminal, dentro da pasta do projeto:

    ```bash
    # 1. Criar o ambiente
    python -m venv venv

    # 2. Ativar o ambiente
    # No Windows (PowerShell):
    .\venv\Scripts\activate
    # No Linux / macOS:
    source venv/bin/activate
    ```

    > ✅ **Sucesso:** A linha do seu terminal agora começa com `(venv)`.

2.  **Instale o Conector `psycopg2`**
    Com o ambiente ativado, instale a biblioteca que faz a ponte entre Python e PostgreSQL:

    ```bash
    pip install psycopg2-binary
    ```

#### 🚨 Resolvendo o Erro de Política de Execução no PowerShell

> Se ao tentar ativar o `venv` no Windows você receber um erro de **`UnauthorizedAccess`** ou **"execução de scripts foi desabilitada"**, isso é uma trava de segurança padrão.
>
> **Solução:**
>
> 1.  Abra o **PowerShell** como **Administrador**.
> 2.  Execute o comando: `Set-ExecutionPolicy RemoteSigned`
> 3.  Confirme digitando `S` e pressionando Enter.
> 4.  Feche o PowerShell de administrador e tente ativar o `venv` novamente em um terminal normal.

-----

### 📄 Passo 2: O Script de Aplicação (`app.py`)

Crie um arquivo `app.py` na raiz do projeto. Este código contém a lógica completa para conectar, buscar e formatar os dados.

```python
import psycopg2
import psycopg2.extras

# --- 1. CONFIGURAÇÕES DE CONEXÃO ---
# ⚠️ ATENÇÃO: Verifique se todos os dados abaixo estão corretos!
# O nome do banco, usuário e principalmente a SENHA.
DB_CONFIG = {
    "host": "localhost",
    "port": "5432",
    "dbname": "petsaude_vca",
    "user": "petsaude_user",
    "password": "uma_senha_bem_forte_aqui" # <-- TROQUE PELA SENHA QUE VOCÊ CRIOU! (no nosso caso foi P3t-S4ud3)
}

# --- 2. CONSULTA SQL COM JUNÇÕES (JOINS) ---
RELATORIO_ATENDIMENTOS_QUERY = """
SELECT
    p.no_paciente,
    s.ds_sexo,
    EXTRACT(YEAR FROM AGE(p.dt_nascimento)) AS idade,
    u.no_unidade,
    a.dt_atendimento,
    a.ds_resumo_atendimento
FROM
    tb_atendimento AS a
JOIN
    tb_paciente AS p ON a.co_paciente = p.co_seq_paciente
JOIN
    tb_unidade_saude AS u ON a.co_unidade_saude = u.co_seq_unidade_saude
JOIN
    dim_sexo AS s ON p.co_sexo = s.co_seq_sexo
WHERE
    u.no_unidade = %s -- Placeholder para a busca segura
ORDER BY
    a.dt_atendimento DESC;
"""

# --- 3. FUNÇÃO PRINCIPAL ---
def gerar_relatorio_por_unidade(nome_unidade):
    """Conecta ao banco, executa a consulta e exibe os resultados."""
    conn = None
    try:
        print(f"Conectando ao banco de dados '{DB_CONFIG['dbname']}'...")
        conn = psycopg2.connect(**DB_CONFIG)
        print("Conexão bem-sucedida!")

        # O RealDictCursor permite acessar os resultados pelo nome da coluna (ex: resultado['no_paciente'])
        cur = conn.cursor(cursor_factory=psycopg2.extras.RealDictCursor)

        print(f"\nBuscando atendimentos para a unidade: '{nome_unidade}'...")
        # A vírgula em (nome_unidade,) é essencial para criar uma tupla de um único elemento
        cur.execute(RELATORIO_ATENDIMENTOS_QUERY, (nome_unidade,))
        resultados = cur.fetchall()
        cur.close()

        if not resultados:
            print("Nenhum atendimento encontrado para esta unidade.")
            return

        print(f"\n--- RELATÓRIO DE ATENDIMENTOS: {nome_unidade} ---")
        for atendimento in resultados:
            print(f"Paciente: {atendimento['no_paciente']} (Idade: {int(atendimento['idade'])}, Sexo: {atendimento['ds_sexo']})")
            print(f"Data: {atendimento['dt_atendimento'].strftime('%d/%m/%Y %H:%M')}")
            print(f"Resumo: {atendimento['ds_resumo_atendimento']}")
            print("-" * 40)
        
        print(f"Total de {len(resultados)} atendimentos encontrados.")

    except psycopg2.Error as e:
        print(f"\n❌ Erro ao interagir com o PostgreSQL: {e}")

    finally:
        if conn is not None:
            conn.close()
            print("\nConexão com o banco de dados fechada.")

# --- 4. PONTO DE ENTRADA DO SCRIPT ---
if __name__ == "__main__":
    # Defina aqui qual unidade de saúde você quer pesquisar
    unidade_de_saude_alvo = "UBS Dr. Régis Pacheco"
    gerar_relatorio_por_unidade(unidade_de_saude_alvo)
```

-----

### ▶️ Passo 3: Executando e Vendo o Resultado

Com tudo pronto, a execução é o passo final.

1.  **Verifique sua Posição:** Certifique-se de que seu terminal está na pasta raiz do projeto (ex: `PET SAUDE`).
2.  **Verifique o Ambiente:** Garanta que o `(venv)` está ativado.
3.  **Execute o Script:**
    ```bash
    python app.py
    ```

O resultado esperado é o relatório completo impresso no seu terminal, provando que a integração foi um sucesso\! 🎉

```bash
(venv) PS C:\Users\joaoh\OneDrive\Documentos\PET SAUDE> python app.py
Conectando ao banco de dados 'petsaude_vca'...
Conexão bem-sucedida!

Buscando atendimentos para a unidade: 'UBS Dr. Régis Pacheco'...

--- RELATÓRIO DE ATENDIMENTOS: UBS Dr. Régis Pacheco ---
Paciente: Ana Clara Guimarães (Idade: 30, Sexo: Feminino)
Data: 09/09/2025 22:03
Resumo: Retorno para mostrar exames. Resultados normais. Aconselhada a manter dieta equilibrada.
----------------------------------------
Paciente: Ana Clara Guimarães (Idade: 30, Sexo: Feminino)
Data: 09/09/2025 22:03
Resumo: Consulta de rotina. Paciente relata bom estado de saúde geral. Aferida pressão arterial: 120/80 mmHg.
----------------------------------------
Total de 2 atendimentos encontrados.

Conexão com o banco de dados fechada.
```



