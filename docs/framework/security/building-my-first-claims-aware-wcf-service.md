---
title: "Criando meu primeiro serviço WCF baseado em declarações"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e0e6d091-9a97-4888-8f2c-cbcee42d90ee
caps.latest.revision: "7"
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.workload: dotnet
ms.openlocfilehash: 791c86b8f833c6b1a8acb6da3b03cfccdafca0e5
ms.sourcegitcommit: c0dd436f6f8f44dc80dc43b07f6841a00b74b23f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/19/2018
---
# <a name="building-my-first-claims-aware-wcf-service"></a>Criando meu primeiro serviço WCF baseado em declarações
## <a name="applies-to"></a>Aplica-se a  
  
-   Windows Identity Foundation (WIF)  
  
-   Windows Communication Foundation (WCF)  
  
## <a name="overview"></a>Visão geral  
 Este tópico descreve o cenário da criação de serviços WCF com reconhecimento de declarações usando o WIF. Geralmente há três participantes em um cenário de serviço Web com reconhecimento de declarações: o serviço Web em si, o usuário final e o STS (Serviço de Token de Segurança). A figura a seguir descreve esse cenário:  
  
 ![Serviço WCF básico baseado em declarações do WIF](../../../docs/framework/security/media/wifbasicclaimsawarewcfservice.gif "WIFBasicClaimsAwareWCFService")  
  
1.  O cliente do serviço WCF (às vezes chamado de agente) usa o WIF para enviar credenciais ao STS e, após a autenticação bem-sucedida, o agente receberá um token do STS.  
  
2.  O agente envia esse token emitido pelo STS para o serviço WCF.  
  
3.  O serviço WCF com reconhecimento de declarações é configurado para usar o STS e os tokens que ele emite. O serviço WCF com reconhecimento de declarações usa o WIF para validar o token e analisá-lo. Os desenvolvedores usam a API e os tipos do WIF, por exemplo, **ClaimsPrincipal**, apropriados para as necessidades do aplicativo, como implementar a autorização para ele.  
  
 A partir do .NET 4.5, o WIF faz parte do pacote do .NET Framework. Ter as classes do WIF diretamente disponíveis no Framework permite uma integração muito mais profunda da identidade baseada em declarações no .NET, facilitando o uso de declarações. Com o WIF 4.5, você não precisa instalar os componentes fora da banda para começar a desenvolver aplicativos Web com reconhecimento de declarações. As classes WIF agora são difundidas por vários assemblies, sendo os principais System.Security.Claims, System.IdentityModel e System.IdentityModel.Services.  
  
 STS é um serviço que emite tokens após a autenticação bem-sucedida. A Microsoft oferece dois STSs padrão do setor:  
  
-   [Serviços de Federação do Active Directory (AD FS) 2.0](http://go.microsoft.com/fwlink/?LinkID=247516) (http://go.microsoft.com/fwlink/?LinkID=247516)  
  
-   [ACS (Serviço de Controle de Acesso) do Microsoft Azure](http://go.microsoft.com/fwlink/?LinkID=247517) (http://go.microsoft.com/fwlink/?LinkID=247517).  
  
 O AD FS 2.0 faz parte do Windows Server R2 e pode ser usado como um STS para cenários locais. O Controle de Acesso do Azure Active Directory (também conhecido como Serviço de Controle de Acesso ou ACS) é um serviço de nuvem, oferecido como parte do Microsoft Azure. Para fins de testes ou educativos, você também pode usar outros STSs para criar seus aplicativos com reconhecimento de reivindicações. Por exemplo, você pode usar o STS de Desenvolvimento Local que faz parte da [Ferramenta de Identidade e Acesso para o Visual Studio](http://go.microsoft.com/fwlink/?LinkID=245849) (http://go.microsoft.com/fwlink/?LinkID=245849), que está disponível online gratuitamente.  
  
 Para criar seu primeiro serviço WCF baseado em declarações usando o WIF, consulte [Como criar um serviço WCF baseado em declarações usando o WIF](http://msdn.microsoft.com/library/431e6415-62ed-4a9f-af03-f14d2b4dfe6d).  
  
## <a name="see-also"></a>Consulte também  
 [Introdução ao WIF](../../../docs/framework/security/getting-started-with-wif.md)
