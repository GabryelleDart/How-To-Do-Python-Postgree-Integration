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

### 🔐 Configuração da Senha

| Sistema Operacional | Usuário Padrão | Configuração de Senha | Comandos |
|---------------------|----------------|------------------------|----------|
| **🪟 Windows** | `postgres` | Definida durante a instalação | *Senha configurada no processo de instalação* |
| **🐧 Linux** | `postgres` (usuário do sistema) | Deve ser definida manualmente | ```sudo -i -u postgres psql \password postgres``` |
| **🍎 macOS** | Mesmo usuário do sistema | Acesso sem senha por padrão | ```psql CREATE USER meu_usuario WITH PASSWORD 'minha_senha';``` |

---

## Criar banco de dados e usuário para o projeto

-----

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

#### 🔵 PSDN-34: Inserção, Atualização e Remoção (DML)

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



