# Integração de Abastecimentos

A integração de abastecimentos é um recurso do CRTI ERP que facilita a comunicação entre o sistema e outras ferramentas, como softwares de gestão de combustíveis, bombas de abastecimento, entre outros. Este recurso garante a atualização contínua dos dados dos postos de combustível, proporcionando informações precisas e atualizadas para a tomada de decisões.

---

## Visão Negocial

O principal objetivo do sistema de abastecimento é a integração automática dos dados provenientes dos postos de combustível, incluindo movimentações de materiais como Diesel S10/S500, aditivos e óleos. Com isso, a gestão do estoque e das operações se torna mais eficiente, otimizando o fluxo de informações e facilitando a análise dos dados.

---

## Requisição Automática

A integração automática é realizada a cada 10 minutos, em intervalos fixos (por exemplo, 8:10, 8:20, etc.), ao longo das 24 horas (das 00:00:00 às 23:59:59). Durante esse processo, o sistema consulta e integra os dados de abastecimento disponíveis no posto de combustível diretamente no CRTI ERP.

> **Nota:**  
> Também é possível executar a integração manualmente de forma retroativa, utilizando o botão de "reimportar". Isso é útil, por exemplo, quando um novo posto é cadastrado e há necessidade de importar dados históricos correspondentes ao período desejado.

> **Beta:**  
> Existe uma versão *beta* que processa os lotes em fila, ao invés de processá-los todos de uma vez, visando melhorar a performance e a escalabilidade do sistema.

---

## Requisitos

Para a correta configuração e funcionamento da integração, é necessário:

- **Configuração da Filial:**  
  Definir a filial onde será realizado o cadastro. Cada filial pode ter apenas uma configuração vinculada.

- **Dados de Integração:**
    - URL de integração
    - Número do posto
    - Token de acesso (quando a API exigir)
    - Login e senha (quando a API exigir)

---

## APIs Disponíveis

O sistema integra com diversas APIs e também oferece integrações via Excel:

1. **CTA:** Integração com a API da CTA.
2. **GTFrota:** Integração com a API da GTFrota.
3. **Evoluma:** Integração com a API da Evoluma.
4. **Polisoftware:** Integração com a API da Polisoftware.
5. **Ticket Log:** Integração via Excel (manual).
6. **Ionics:** Integração via Excel (manual).

> **Observação:**  
> As integrações via Excel (Ticket Log e Ionics) são executadas somente de forma manual.

---

## Fluxo de Requisição

1. **Requisição:**  
   A solicitação é enviada e, se for bem-sucedida, os dados retornados passam para a próxima etapa.

2. **Tratamento de Dados:**  
   São processadas informações como quantidade abastecida, placa, horímetro, odômetro, entre outras.

3. **Processamento:**  
   Os dados são integrados à filial correspondente ao lote mestre de abastecimentos, que deve coincidir com a configuração previamente definida.

---

## Fluxos de Processamento

Após o tratamento dos dados, o processamento pode seguir dois caminhos:

1. **Saída de Estoque:**  
   Verifica a quantidade disponível e gera a saída de estoque correspondente.

2. **Entrada de Estoque:**  
   Gera a entrada de estoque, garantindo a atualização dos registros.
   > **Nota:** Este fluxo é gerenciado pelo mesmo processo de BEM-I e BSM-I, não sendo tratado diretamente pelo módulo de abastecimento.

---

**Documentação referente à data de criação: 05/03/2025**
