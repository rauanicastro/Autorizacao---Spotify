# Autorização


A autorização acontece quando um usuário ou aplicativo pede permissão para acessar dados e features do Spotify. O protocolo de autorização utilizado pelo Spotify é o [OAuth 2.0](https://datatracker.ietf.org/doc/html/rfc6749).

![](https://i.imgur.com/YwHPe20.png)

### Visão geral

O processo de autorização requer credenciais válidas do cliente, sendo elas as chaves `client ID` e `client secret`.

>Para saber como gerar as chaves `client ID` e `client secret`, leia o [guia de configurações do aplicativo](https://developer.spotify.com/documentation/general/guides/authorization/app-settings/).

Além disso, o acesso aos recursos protegidos é determinado por um ou mais escopos. O escopo permite que o aplicativo acesse funcionalidades específicas (como ler uma playlist, modificar a biblioteca ou dar stream) em nome de um usuário. O conjunto de escopos definidos durante a autorização determina as permissões de acesso que o usuário é solicitado a conceder.

> As informações detalhadas sobre os escopos de autorização podem ser encontradas no [guia de escopos](https://developer.spotify.com/documentation/general/guides/authorization/scopes/).

Depois que a autorização é concedida, o servidor da autorização fornece um token de acesso que é usado para fazer chamadas de API em nome do usuário ou do aplicativo.

O padrão do OAuth2 define quatro fluxos de concessões para solicitar e obter um token de acesso. Os implementados pelo Spotify são:

-   [Código de autorização](https://developer.spotify.com/documentation/web-api/tutorials/code-flow)
- [Código de autorização com extensão PKCE](https://developer.spotify.com/documentation/web-api/tutorials/code-pkce-flow)
-   [Credenciais do cliente](https://developer.spotify.com/documentation/web-api/tutorials/client-credentials-flow)
-   [Concessão implícita](https://developer.spotify.com/documentation/web-api/tutorials/implicit-flow)

### Qual fluxo do OAuth2 usar

Para uma maior segurança, você deve optar pelo fluxo mais compatível com o tipo de aplicativo que está sendo criado.

 - Se você está desenvolvendo um aplicativo de execução longa (como um aplicativo web em execução no servidor) em que o usuário concede permissão apenas uma vez e o `client secret` pode ser armazenado com segurança, o fluxo de **[código de autorização](https://developer.spotify.com/documentation/general/guides/authorization/code-flow/)** é o recomendado.
 - Quando não é possível armazenar o `client secret` de modo confiável (desktop, aplicativos mobile ou aplicativos web em JavaScript executados no navegador), a melhor escolha pode ser o **[código de autorização com PKCE](https://developer.spotify.com/documentation/general/guides/authorization/code-flow/)**, já que esse fluxo protege contra ataques em que o código de autorização pode ser interceptado.
 - Para alguns aplicativos executados no back-end, como CLIs ou daemons, o sistema autentica e autoriza um aplicativo em vez de um usuário. Nesses casos, as **[credenciais do cliente](https://developer.spotify.com/documentation/general/guides/authorization/client-credentials/)** são o tipo de fluxo mais escolhido.  Esse fluxo não inclui autorização do usuário, portanto, apenas endpoints que não solicitam informações do usuário podem ser acessados.
 - Já a **[concessão implícita](https://developer.spotify.com/documentation/general/guides/authorization/implicit-grant)** **não é recomendada** por ser um fluxo com desvantagens consideráveis, como retornar o token no URL em vez de um canal confiável, além de não fornecer suporte a refresh tokens. 

| FLUXO | ACESSO AOS RECURSOS DO USUÁRIO | REQUER CHAVE SECRETA (_server_-_side_) | REFRESH TOKEN |
:---: | :---: | :---: | :---: | 
| Código de autorização | Sim | Sim | Sim |
| Código de autorização com PKCE | Sim | Não | Sim |
| Credenciais do cliente | Não | Sim | Não |
| Concessão implícita | Sim | Não | Não |


 
