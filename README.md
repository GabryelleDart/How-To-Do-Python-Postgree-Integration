# How-To-Do-Python-Postgree-Integration

## 📖 Sobre o Projeto


---
## Estrutura 
----
## 🚀 O que é o PostgreSQL?

O **PostgreSQL** (ou apenas *Postgres*) é um **banco de dados relacional**.  
Isso significa que ele armazena informações em **tabelas organizadas**, permitindo relacionar dados entre si de forma lógica e eficiente.  

👉 Imagine uma planilha do Excel com várias abas (tabelas), mas muito mais poderosa, rápida e segura.  

### 🔑 Principais características:
- **Gratuito e Open Source**: você não paga licença para usar.
- **Seguro**: possui autenticação por senha e criptografia.
- **Escalável**: funciona bem em pequenos projetos e em grandes empresas.
- **Flexível**: pode lidar com números, textos, arquivos JSON, localização geográfica e muito mais.

### 🛠️ Onde o PostgreSQL é usado?
- Sistemas de gestão de empresas (ERP, CRM).
- Aplicações web e APIs (Java, Python, Node.js, etc).
- Ciência de dados e análise de grandes volumes de informação.
- Apps de celular que precisam salvar informações de usuários.
- Plataformas como **Instagram** e **Spotify** usam bancos de dados relacionais semelhantes.
----
## Como instalar o PostgreSQL no ambiente de desenvolvimento
Acesse https://www.postgresql.org/download/
<img width="1919" height="910" alt="Captura de tela 2025-09-09 165154" src="https://github.com/user-attachments/assets/2cecbfd9-50f7-40f9-b562-2a0533cc8fc1" />
Escolha de acordo ao seu Sistema Operacional
Clique em 'Dowload the installer'
<img width="1919" height="899" alt="image" src="https://github.com/user-attachments/assets/c339ba4f-6f9e-46f7-9d4b-3836aa4d8b7c" />
Voce será direcionado para https://www.enterprisedb.com/downloads/postgres-postgresql-downloads onde poderá escolher a versao do Postgre e baixar conforme seus Sistema operacional
<img width="1916" height="909" alt="image" src="https://github.com/user-attachments/assets/0ae0f12c-397b-4c94-83bc-3f0cda8c08b9" />
Execute o instalador:
   - Selecione os componentes: **PostgreSQL Server, pgAdmin 4, Command Line Tools**.  
   - Crie uma senha para o usuário **postgres** (é o "administrador do banco").  
   - Deixe a porta padrão: `5432`.
  Obs: Normalmente el sugerirá a porta `5432` mas caso haja diferença é por conta desse porta já estra sendo usada por outra aplicação.
   - Conclua a instalação.
 Teste se funcionou:
   - Abra o **Prompt de Comando (CMD)** e digite:
     ```bash
     psql --version
     ```
     <img width="1472" height="618" alt="Captura de tela 2025-09-09 171015" src="https://github.com/user-attachments/assets/82f3b355-83b8-40bd-a8be-a55409bd5b94" />

   - Se não reconhecer, adicione o caminho `C:\Program Files\PostgreSQL\<versão>\bin` às **variáveis de ambiente** do Windows.
-------------
Configurar o PostgreSQL para acesso local seguro
Criar banco de dados e usuário para o projeto
