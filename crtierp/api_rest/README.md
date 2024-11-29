# API REST do CRTI ERP

A seguir será descrita a API REST do CRTI ERP, seu ciclo de vida, e como utiliza-la. O Swagger da API pública pode ser visualizada em *https://endereco_da_app/api*, com o usuário logado no ERP. Existem 2 tipos de autenticação com o ERP, via login e senha e via chave de autenticação. Para novos softwares clientes do ERP, como aplicativos ou frontends, utilizar a API de login e senha. Para aplicações B2B (Business to Business), utilizar chave de autenticação.

Alguns exemplos de utilização:

- ***Chave de Autenticação***: Integração com outros ERP, integração com softwares de BI, integração com CRM, etc.
- ***Login e senha (Request/Refresh Tokens)***: Aplicativos para smartphones/tablets, software desktop, frontend customizado para o ERP, etc.

## Ciclo para Utilização da API Pública REST do CRTI ERP via chave de integração

A chave de integração pode ser gerada no ERP em *Configurações do Sistema > Permissões > Usuário*. Deve se editar um usuário, e na tela de cadastro, clicar me *Chaves (API)*. Nessa tela, selecione *Gerar chave*, dê um nome que identifique o uso da chave. A chave irá ser exibida apenas 1x. Ao fechar janela, se necessitar da chave novamente, será que invalidar e gerar uma nova. Armazenar a chave gerada de forma segura. Evitar guarda-la em arquivos texto ou em meios não criptografados.

Para utilizar a chave, deverá ser enviado o header `X-API-Key` em cada requisição, informando a chave gerada.

**Exemplo de cabeçalho com chave de autenticação:**
```http
GET /api/v1/modelo/recurso
X-API-Key: chave_de_autenticacao
```

## Ciclo para Utilização da API Pública REST do CRTI ERP via login e senha

A utilização da API Pública REST do CRTI ERP segue um fluxo bem definido que permite a autenticação e a continuidade da comunicação segura entre o cliente e o servidor. A seguir, descrevemos cada passo necessário. O fluxo deverá ser utilizado como o recomendado, para o correto funcionamento da aplicação e evitar bloqueios por consumo indevido da API. 

### 1. Autenticação Inicial (Endpoint de signin)
O primeiro passo no ciclo de utilização da API é a autenticação do usuário. Utilizando o endpoint de `signin`, você deverá enviar as credenciais do usuário (como nome de usuário e senha) para obter um **request token**. Este token é utilizado para autorizar todas as requisições subsequentes à API.

**Exemplo de chamada ao endpoint de sigin:**
```http
POST /api/v1/auth/signin
Content-Type: application/json
{
  "username": "seu_usuario",
  "password": "sua_senha"
}
```

**Exemplo de resposta ao endpoint de sigin:**
```http
{
  "accessToken": "Token de Acesso válido por 15 minutos.",
  "refreshToken": "Token de Refresh válido por 1 dia."
}
```

#### 2. Utilização do Request Token
Após a autenticação bem-sucedida, você receberá um **request token** que será incluído no cabeçalho de todas as requisições subsequentes para autorizar o acesso aos recursos da API. O request token tem a validade de 15 minutos.

**Exemplo de cabeçalho com request token:**
```http
GET /api/v1/modelo/recurso
Authorization: Bearer seu_request_token
```

#### 3. Renovação do Token (Endpoint de Refresh Token)
Os request tokens têm um tempo de validade limitado. Para evitar a necessidade de autenticar novamente o usuário após o token expirar, a API fornece um mecanismo de renovação através do endpoint de `refresh token`. Utilizando o refresh token recebido inicialmente, você pode obter um novo *request token* e um novo *refresh token*. Após a utilização do *refresh token*, o mesmo é invalidado, necessitando utilizar o novo *refresh token* na próxima renovação.

**Exemplo de chamada ao endpoint de Refresh Token:**
```http
POST /api/v1/auth/refresh_token
Content-Type: application/json
{
  "refreshToken": "seu_refresh_token"
}
```


**Exemplo de resposta ao endpoint de refresh token:**
```http
{
  "accessToken": "Token de Acesso válido por 15 minutos.",
  "refreshToken": "Token de Refresh válido por 1 dia."
}
```

#### 4. Continuidade da Sessão
Ao receber um novo request token através do endpoint de refresh token, você deve utilizá-lo para continuar acessando os recursos da API. Este ciclo de renovação pode ser repetido enquanto o refresh token atual permanecer válido, garantindo uma sessão contínua e segura.

### Request Tokens vs. Refresh Tokens

- **Request Tokens**: São tokens de curta duração utilizados para autenticar as requisições à API. Eles garantem que cada requisição é autorizada de maneira segura.
- **Refresh Tokens**: São tokens de longa duração utilizados exclusivamente para obter novos request tokens quando os tokens atuais expirarem. Eles permitem manter a sessão ativa sem a necessidade de solicitar credenciais de usuário repetidamente.

Este ciclo garante uma comunicação segura e contínua entre o cliente e o servidor, minimizando o risco de acesso não autorizado e melhorando a experiência do usuário.

