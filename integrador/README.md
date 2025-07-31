# Integração Usina de Concreto

<p align="center">
  <img src="img/logoCrtiErp.png" alt="Logo CrtiErp" width="200"/>
</p>

Este projeto consiste no software responsável por integrar as operações de entrada e saída da Usina de Concreto com o CRTI ERP.

***

## Softwares Homologados

- **INSTAL**
- **SAUC**
- **SAI**
- **API REST**
- **COMMAND ALKON** 
- **SHM**

***

## Instalação e Configuração

### 1. Configuração Inicial

Para iniciar o envio de informações da usina para o CRTI ERP, é necessário realizar a configuração na máquina designada para esse fim.

### 2. Download do Arquivo

- **Arquivo Disponível:** [Integração Usina](https://crticombr-my.sharepoint.com/:f:/g/personal/carlos_crti_com_br/Eh4-ALBzhVdGq7UvYpObVzgBCUgO7t5OL3j8TyXXyL1NBA?e=Vhym74)
  > **Observação:**  
  > O arquivo está disponível no SharePoint da CRTI. Caso não tenha acesso, entre em contato com o suporte.  
  > Recomenda-se sempre realizar o download da versão mais recente.

### 3. Pré-requisitos

- **Java 17:**  
  Certifique-se de que o Java na versão 17 esteja instalado na máquina.  
  Faça o download em: [Adoptium Temurin Releases](https://adoptium.net/temurin/releases/?os=windows&package=jre&arch=x64)

### 4. Instalação e Configuração no Windows

Siga os passos abaixo para instalar e configurar o integrador no ambiente Windows:

1. **Instalação da JRE:**
    - Baixe e instale a JRE versão 17 a partir do link fornecido.

2. **Descompactar Arquivos:**
    - Extraia o conteúdo do arquivo `.zip` para o diretório:  
      `C:\integradorcrti`

3. **Instalação do Serviço:**
    - Execute o arquivo `instalar_servico.bat` para instalar o serviço no computador.

4. **Iniciar o Serviço:**
    - Abra a ferramenta de serviços do Windows (digite "serviços" na pesquisa do Windows).
    - Localize e inicie o serviço denominado **CRTI Integrador Usina Concreto**.]
    - Após a Configuração da comunicação é necessário reniciar o serviço.

5. **Acessar a Interface Web:**
    - Abra o navegador e acesse: [http://localhost:5000](http://localhost:5000).

6. **Configuração Inicial:**
    - Preencha os campos da interface de acordo com as informações da sua empresa.

> **Observação:**  
> As configurações são salvas em um banco de dados embutido (HSQLDB), localizado no diretório do usuário:
> - **Windows:** `C:\Users\[nome do usuário]\.crtierp` ou `~/.crtierp`
> - **Linux:** `/home/[nome do usuário]/.crtierp`

***

## Descrição dos Campos de Configuração Comunicação

- **URL do ERP:**  
  Informe a URL do sistema ERP a ser integrado.  
  *Exemplo:* `xxx.crti.com.br` (não inclua o protocolo `http://` ou `https://`).

- **Token do ERP:**  
  Token de acesso gerado para a integração.  
  Para gerar o token, acesse a tela de Usuários, clique em **Chaves (API)** e gere uma chave.
  > **Nota:** O token é gerado apenas uma vez. Após fechar a aba, não é possível copiá-lo novamente.  

- **Utiliza SSL?:**  
  Indica se a comunicação entre o integrador e o ERP será realizada via SSL.
  > **Nota:** Em Ambiente de produção devera sempre estar ativado.

## Descrição dos Campos de Configuração

- **Tipo de Integração:**  
  Define o layout de integração a ser utilizado.

- **Código do Ponto de Carga:**  
  Código de integração do Ponto de Carga, correspondente ao valor informado no campo “Código de Integração” do Ponto de Carga dentro do CRTIerp.  

- **Diretório de Remessa:**  
  Local onde o sistema salvará os arquivos de remessa.

- **Diretório de Retorno:**  
  Local onde o sistema da usina do cliente armazenará os arquivos de retorno.

> **Nota:**  
> Todos os campos são obrigatórios para a configuração correta do sistema.

***

## Utilização do Serviço

Após a configuração, o uso do serviço é simples:

1. **Envio de Dados:**
    - No módulo **Saída de Material**, acesse a seção **Integração**.
    - Clique em **Enviar para Integração Usina** para que o arquivo seja gerado automaticamente na pasta de destino configurada.
***

**Documentação referente à data de criação: 30/07/2025**
<p align="center">
  <img src="img/logoCrtiErp.png" alt="Logo CrtiErp" width="200"/>
</p>