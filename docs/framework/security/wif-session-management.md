---
title: "Gerenciamento de sessões do WIF"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 98bce126-18a9-401b-b20d-67ee462a5f8a
caps.latest.revision: "7"
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.workload: dotnet
ms.openlocfilehash: 7703d9fb612ead13140d010b1670abb209c5acb7
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/22/2017
---
# <a name="wif-session-management"></a>Gerenciamento de sessões do WIF
Quando um cliente tenta acessar um recurso protegido hospedado por uma terceira parte confiável pela primeira vez, o cliente deve primeiro se autenticar em um STS (serviço de token de segurança) que é de confiança da terceira parte confiável. Em seguida, o STS emite um token de segurança para o cliente. O cliente apresenta esse token para a terceira parte confiável, que, em seguida, concede o acesso do cliente ao recurso protegido. No entanto, você não deseja que o cliente precise se autenticar novamente no STS a cada solicitação, especialmente, porque ele até mesmo pode não estar no mesmo computador ou no mesmo domínio da terceira parte confiável. Em vez disso, o WIF (Windows Identity Foundation) faz com que o cliente e a terceira parte confiável estabeleçam uma sessão em que o cliente usa um token de segurança de sessão para se autenticar na terceira parte confiável para todas as solicitações após a primeira solicitação. A terceira parte confiável pode usar esse token de segurança de sessão, que é armazenado em um cookie, para reconstruir o <xref:System.Security.Claims.ClaimsPrincipal?displayProperty=nameWithType> do cliente.  
  
 O STS define qual autenticação o cliente deve fornecer. No entanto, o cliente pode ter várias credenciais com as quais ele pode se autenticar no STS. Por exemplo, ele pode ter um token do Windows Live, um nome de usuário e uma senha, um certificado e uma chave inteligente. Nesse caso, o STS concede ao cliente várias identidades, com cada identidade correspondendo a uma das credenciais apresentadas pelo cliente. A terceira parte confiável pode usar uma ou mais dessas identidades quando decidir qual nível de acesso será concedido ao cliente.  
  
 A <xref:System.IdentityModel.Tokens.SessionSecurityToken?displayProperty=nameWithType> é usada para reconstruir o <xref:System.Security.Claims.ClaimsPrincipal?displayProperty=nameWithType> do cliente, que contém todas as identidades do cliente em <xref:System.Security.Claims.ClaimsPrincipal.Identities%2A>. Cada <xref:System.Security.Claims.ClaimsIdentity?displayProperty=nameWithType> na coleção contém os tokens de inicialização associados a essa identidade.  
  
 Se um novo token de sessão é emitido com a ID de sessão do token de sessão original, <xref:System.IdentityModel.Tokens.SessionSecurityTokenHandler?displayProperty=nameWithType> não atualiza o token de sessão no cache de token. Você sempre deve instanciar um token de sessão com uma ID de sessão exclusiva.  
  
> [!NOTE]
>  Session.SecurityTokenHandler.ReadToken gera uma exceção <xref:System.Xml.XmlException> se ela recebe uma entrada inválida; por exemplo, se o cookie que contém o token de sessão está corrompido. Recomendamos capturar essa exceção e fornecer um comportamento específico ao aplicativo.  
  
 Se uma página da Web protegida contiver muitos recursos (como gráficos pequenos) que também estão no domínio protegido, o cliente deverá se autenticar novamente na terceira parte confiável para baixar cada um desses recursos. O uso de um token de autenticação de sessão evita a necessidade de se autenticar no STS a cada solicitação, mas ainda significa que muitos cookies estão sendo enviados. Talvez você deseje configurar a página da Web para que os dados e os recursos importantes sejam armazenados no domínio protegido, enquanto itens secundários são armazenados em um domínio desprotegido e vinculados por meio da página da Web principal. Além disso, defina o caminho do cookie para referenciar somente o domínio protegido.  
  
 Para operar no modo de referência, a Microsoft recomenda fornecer um manipulador para o evento <xref:System.IdentityModel.Services.WSFederationAuthenticationModule.SessionSecurityTokenCreated> no arquivo **global.asax.cs** e configurar a propriedade **IsReferenceMode** no token passado na propriedade <xref:System.IdentityModel.Services.SessionSecurityTokenCreatedEventArgs.SessionToken%2A>. Essas atualizações garantirão que o token de sessão opere em modo de referência para cada solicitação e são preferíveis em comparação a simplesmente configurar a propriedade <xref:System.IdentityModel.Services.SessionAuthenticationModule.IsReferenceMode%2A> no Módulo de Autenticação de Sessão.  
  
## <a name="extensibility"></a>Extensibilidade  
 É possível estender o mecanismo de gerenciamento de sessão. Um motivo para isso seria melhorar o desempenho. Por exemplo, você pode criar um manipulador de cookie personalizado que transforma ou otimiza o token de segurança de sessão entre seu estado na memória e o que acontece no cookie. Para fazer isso, configure a propriedade <xref:System.IdentityModel.Services.SessionAuthenticationModule.CookieHandler%2A?displayProperty=nameWithType> da <xref:System.IdentityModel.Services.SessionAuthenticationModule?displayProperty=nameWithType> para usar um manipulador de cookie personalizado que é derivado de <xref:System.IdentityModel.Services.CookieHandler?displayProperty=nameWithType>. <xref:System.IdentityModel.Services.ChunkedCookieHandler?displayProperty=nameWithType> é o manipulador de cookie padrão, pois os cookies excedem o tamanho permitido para o protocolo HTTP; se, em vez disso, você usar um manipulador de cookie personalizado, deverá implementar o agrupamento.  
  
 Para obter mais informações, consulte a amostra [ClaimsAwareWebFarm](http://go.microsoft.com/fwlink/?LinkID=248408) (http://go.microsoft.com/fwlink/?LinkID=248408). Essa amostra apresenta um cache de sessão pronto para o farm (em vez de um tokenreplycache), para que você possa usar sessões por referência, em vez de trocar cookies grandes. Essa amostra também apresenta uma maneira mais fácil de proteger cookies em um farm. O cache de sessão é baseado no WCF. Em relação à proteção da sessão, a amostra apresenta uma nova funcionalidade no WIF 4.5 de uma transformação de cookie baseada em MachineKey, que pode ser ativada simplesmente colando o trecho apropriado no web.config. O exemplo em si não está em um farm, mas demonstra o que você precisa para tornar seu aplicativo pronto para o farm.
