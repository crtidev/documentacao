-----

# Guia de Manutenção e Solução de Problemas: Integrador Usina Concreto 

<p align="center">
  <img src="imagens/logoCrti.jpg" alt="Logo CrtiErp" width="200"/>
</p>

## Cenário de Aplicação

Este procedimento padrão deve ser executado quando o serviço `Integrador Usina Concreto` falha ao iniciar e os seguintes erros são identificados no arquivo de log `usinaconcreto.wrapper.log`:

> `ERROR - Failed to start service.` 
> `System.ComponentModel.Win32Exception: O sistema não pode encontrar o arquivo especificado.` 

## Diagnóstico do Problema

A análise dos erros indica duas causas raiz possíveis:

1.  **Corrupção de Dados:** Os arquivos físicos do banco de dados embarcado podem estar corrompidos, impedindo a inicialização da aplicação.
2.  **Configuração de Ambiente:** O executável `java.exe` não é encontrado pelo contexto de execução do serviço Windows.

A solução consiste em corrigir a configuração do serviço e limpar os dados da aplicação para garantir uma reinicialização limpa.

## Visão Geral da Solução

A resolução completa é alcançada através da execução de duas etapas principais:

1.  **Configuração do Serviço:** Edição do arquivo `usinaconcreto.xml` para incluir o caminho absoluto do executável `java.exe`.
2.  **Reset da Aplicação:** Utilização do script `reinstalar_servico.bat` para automatizar a desinstalação, limpeza de dados e reinstalação do serviço.

-----

## Procedimento Operacional Padrão

### **Etapa 1: Identificação e Configuração do Ambiente Java**

O objetivo desta etapa é garantir que o serviço localize o ambiente de execução Java. Este procedimento de configuração é executado apenas uma vez.

**a) Abrir o Windows PowerShell** 

- Pressione a tecla **Windows**, digite `PowerShell` e selecione **"Windows PowerShell"**.

**b) Identificar o Caminho do Executável Java** 

- No terminal do PowerShell, execute o seguinte comando:
  ```powershell
  Get-Command java.exe | Select-Object -ExpandProperty Source
  ```
- O comando retornará o caminho completo do arquivo `java.exe`.

> - **Java 17:**  
    Certifique-se de que o Java na versão 17 esteja instalado na máquina.  
    Faça o download em: [Adoptium Temurin Releases](https://adoptium.net/temurin/releases/?os=windows&package=jre&arch=x64)

**c) Copiar o Caminho** 

- Selecione a linha de texto do caminho retornado e copie-a para a área de transferência (Ctrl + C).

**d) Acessar o Arquivo de Configuração** 

- Navegue até o diretório da aplicação.
- Abra o arquivo `usinaconcreto.xml` com um editor de texto (ex: Bloco de Notas).

**e) Atualizar o Arquivo de Configuração** 

- Substitua todo o conteúdo do arquivo `usinaconcreto.xml` pelo modelo abaixo:

  ```xml
  <service>
    <id>crtiintegradorusina</id>
    <name>CRTI Integrador Usina Concreto</name>
    <description>Este servico integra a usina de concreto.</description>
    
    <executable>SEU_CAMINHO_DO_JAVA_AQUI</executable>
    
    <arguments>-jar "integradorusinaconcreto.jar"</arguments>
    <logmode>rotate</logmode>
  </service>
  ```

- Cole o caminho do Java copiado no passo (c), substituindo o texto `SEU_CAMINHO_DO_JAVA_AQUI`.

  *Exemplo de configuração final:*

  ```xml
  <executable>C:\Program Files\Java\jdk-17\bin\java.exe</executable>
  ```

- Salve e feche o arquivo.

### **Etapa 2: Execução do Script de Reinstalação de Serviço**

Com a configuração corrigida, execute o script para aplicar as alterações e reiniciar a aplicação.

1.  Navegue até o diretório da aplicação.
2.  Localize o arquivo de lote **`reinstalar_servico.bat`**.
3.  Clique com o botão direito do mouse sobre o arquivo e selecione **"Executar como administrador"**.
4.  Na tela do prompt de comando, confirme a execução digitando `S` e pressionando **Enter**.
5.  Aguarde a finalização do script, que exibirá a mensagem de sucesso ao final.

Após a conclusão, o serviço estará reinstalado e operacional.

---

<p align="center">
  <img src="imagens/logoCrti.jpg" alt="Logo CrtiErp" width="200"/>
</p>