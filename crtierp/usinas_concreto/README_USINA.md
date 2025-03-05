# Integração Usina de Concreto

Este projeto consiste no software responsável pela integração das operações de entrada e saída da Usina de Concreto com o CRTI ERP, permitindo uma comunicação fluida entre os sistemas.

---

## Softwares Homologados

- **INSTAL**
- **SAUC**
- **SAI**
- **API REST**
- **COMMAND ALKON** (Em Desenvolvimento)

---

## Instalação e Configuração

### 1. Configuração Inicial

Para iniciar o envio de informações da usina para o CRTI ERP, é necessário realizar a configuração na máquina designada para esse fim.

### 2. Download do Arquivo

- **Arquivo Disponível:** `Integração Usina`

### 3. Pré-requisitos

- **Java 17:**  
  Certifique-se de que o Java na versão 17 esteja instalado na máquina.  
  Faça o download em: [Adoptium Temurin Releases](https://adoptium.net/temurin/releases/?os=windows&package=jre&arch=x64)

### 4. Instalação e Configuração no Windows

Siga os passos abaixo para instalar e configurar o integrador no Windows:

1. **Instalação da JRE:**  
   Instale a JRE na versão 17. Ela pode ser baixada através do link acima.

2. **Descompactar Arquivos:**  
   Extraia o conteúdo do arquivo `.zip` para o diretório `C:\integradorcrti`.

3. **Instalação do Serviço:**  
   Execute o arquivo `instalar_servico.bat` para instalar o serviço no computador.

4. **Iniciar o Serviço:**  
   Inicie o serviço denominado **CRTI Integrador Usina Concreto**.

5. **Acessar a Interface Web:**  
   Abra o navegador e acesse: [http://localhost:5000](http://localhost:5000).

6. **Configuração Inicial:**  
   Configure os campos de acordo com as informações da sua empresa.

> **Observação:**  
> As configurações são salvas em um banco de dados embutido (HSQLDB), localizado no diretório do usuário:
> - **Windows:** `C:\Users\[nome do usuário]\.crtierp` ou `~/.crtierp`
> - **Linux:** `/home/[nome do usuário]/.crtierp`

---

## Descrição dos Campos de Configuração

- **Tipo de Integração:**  
  Define o layout de integração a ser utilizado.

- **URL do ERP:**  
  Informe a URL do sistema ERP a ser integrado (exemplo: `xxx.crti.com.br` – sem o protocolo `http://` ou `https://`).

- **Token do ERP:**  
  Token de acesso gerado para a integração. Acesse a tela de Usuários, clique em **Chaves (API)** e gere uma chave. Recomenda-se criar um usuário exclusivo para a integração com a usina.

- **Código do Ponto de Carga:**  
  Código de integração do Ponto de Carga. Este não é o código sequencial, mas o valor informado no campo “Código de Integração” do Ponto de Carga.

- **Diretório de Remessa:**  
  Local onde o sistema salvará os arquivos de remessa.

- **Diretório de Retorno:**  
  Local onde o sistema da usina do cliente armazenará os arquivos de retorno. Preencha este campo somente se o cliente desejar processar os retornos no ERP.

- **Utiliza SSL?**  
  Indica se a comunicação entre o integrador e o ERP é feita via SSL. Marque a opção por conta do Protocolo de Segurança.

---

**Documentação referente à data de criação: 05/03/2025**