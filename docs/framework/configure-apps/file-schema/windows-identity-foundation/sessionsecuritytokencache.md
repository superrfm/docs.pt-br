---
title: '&lt;sessionSecurityTokenCache&gt;'
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d43e676c-0153-485c-ab31-0257a2db7507
caps.latest.revision: "8"
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.workload: dotnet
ms.openlocfilehash: 9f4b87d6c620a07ee831888086bdab75a689875e
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/22/2017
---
# <a name="ltsessionsecuritytokencachegt"></a>&lt;sessionSecurityTokenCache&gt;
Registra um cache de tokens de sessão com um serviço ou uma coleção de manipulador de token de segurança.  
  
 \<System. IdentityModel >  
\<identityConfiguration >  
\<armazena em cache >  
\<sessionSecurityTokenCache >  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
<system.identityModel>  
  <identityConfiguration>  
    <caches>  
      <sessionSecurityTokenCache type=xs:string>  
      </sessionSecurityTokenCache>  
    </caches>  
  </identityConfiguration>  
</system.identityModel>  
```  
  
## <a name="attributes-and-elements"></a>Atributos e elementos  
 As seções a seguir descrevem atributos, elementos filho e elementos pai.  
  
### <a name="attributes"></a>Atributos  
  
|Atributo|Descrição|  
|---------------|-----------------|  
|tipo|Um tipo que deriva de <xref:System.IdentityModel.Tokens.SessionSecurityTokenCache> classe.|  
  
### <a name="child-elements"></a>Elementos filho  
 Nenhum  
  
### <a name="parent-elements"></a>Elementos pai  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|[\<armazena em cache >](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/caches.md)|Registra os caches usados por um serviço ou uma coleção de manipulador de token de segurança.|  
  
## <a name="example"></a>Exemplo  
 O XML a seguir mostra a configuração de um cache personalizado para manter a sessão de tokens de segurança (<xref:System.IdentityModel.Tokens.SessionSecurityToken>). A configuração é obtida o `ClaimsAwareWebFarm` exemplo. Para obter mais informações sobre esse exemplo, consulte [índice de exemplo de código do WIF](../../../../../docs/framework/security/wif-code-sample-index.md).  
  
```xml  
<caches>  
  <sessionSecurityTokenCache type="CacheLibrary.SharedSessionSecurityTokenCache, CacheLibrary">  
    <!--cacheServiceAddress points to the centralized session security token cache service running in the web farm.-->  
    <cacheServiceAddress url="http://localhost:4161/SessionSecurityTokenCacheService.svc" />  
  </sessionSecurityTokenCache>  
</caches>  
```  
  
## <a name="see-also"></a>Consulte também  
 <xref:System.IdentityModel.Tokens.SessionSecurityTokenCache>
