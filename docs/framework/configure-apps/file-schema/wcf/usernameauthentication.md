---
title: '&lt;userNameAuthentication&gt;'
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 24d8b398-770f-418f-ba23-c4325419cfa6
caps.latest.revision: "10"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: cea18a2c8c2244f384b87b48f195b77da4eb5dfd
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/22/2017
---
# <a name="ltusernameauthenticationgt"></a>&lt;userNameAuthentication&gt;
Especifica as credenciais de um serviço com base no nome de usuário e senha.  
  
 \<sistema. ServiceModel >  
\<comportamentos >  
\<serviceBehaviors >  
\<comportamento >  
\<serviceCredentials >  
\<userNameAuthentication >  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
<userNameAuthentication  
   cacheLogonTokenLifetime="TimeSpan"  
   cacheLogonTokens="Boolean"   
   customUserNamePasswordValidatorType="String"  
   includeWindowsGroups="Boolean"   
   maxCacheLogonTokens="Integer"  
   membershipProviderName="String"  
   userNamePasswordValidationMode="Windows/MembershipProvider/Custom" />  
```  
  
## <a name="attributes-and-elements"></a>Atributos e elementos  
 As seções a seguir descrevem atributos, elementos filho e elementos pai.  
  
### <a name="attributes"></a>Atributos  
  
|Atributo|Descrição|  
|---------------|-----------------|  
|`cacheLogonTokenLifetime`|Um <xref:System.TimeSpan> que especifica o comprimento máximo de tempo que um token é armazenado em cache. O padrão é 00:15:00.|  
|`cacheLogonTokens`|Um valor booleano que especifica se tokens de logon são armazenadas em cache. O padrão é `false`.|  
|`customUserNamePasswordValidatorType`|Uma cadeia de caracteres que especifica o tipo de validador de senha do nome de usuário personalizada a ser usado. O padrão é uma cadeia de caracteres vazia.|  
|`includeWindowsGroups`|Um valor booleano que especifica se os grupos do Windows é incluída no contexto de segurança. O padrão é `true`.<br /><br /> A configuração desse atributo `true` tem um impacto de desempenho que resulta em uma expansão de grupo completo. Defina essa propriedade como `false` se você não precisa estabelecer a lista de grupos de um usuário pertence.|  
|`maxCacheLogonTokens`|Um inteiro que especifica o número máximo de tokens de logon para o cache. Esse valor deve ser maior que zero. O padrão é 128.|  
|`membershipProviderName`|Quando o `clientCredentialType` atributo de uma associação é definido como `username`, o nome de usuário é mapeado para contas do Windows. Você pode substituir esse comportamento usando esse atributo, que é uma cadeia de caracteres que contém o nome do <xref:System.Web.Security.MembershipProvider> valor que fornece o mecanismo de validação de senha relevantes.|  
|`userNamePasswordValidationMode`|Especifica a maneira pela qual nome de usuário de senha é validada. Os valores válidos são:<br /><br /> -Windows<br />-MembershipProvider<br />-Custom<br /><br /> O padrão é Windows. Esse atributo é do tipo <xref:System.ServiceModel.Security.UserNamePasswordValidationMode>.|  
  
### <a name="child-elements"></a>Elementos filho  
 nenhuma.  
  
### <a name="parent-elements"></a>Elementos pai  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|[\<serviceCredentials >](../../../../../docs/framework/configure-apps/file-schema/wcf/servicecredentials.md)|Especifica a credencial a ser usada na autenticação de serviço, e a validação de credencial de cliente as configurações relacionadas.|  
  
## <a name="remarks"></a>Comentários  
 Se nenhuma das associações usadas por um serviço estiver configurada para autenticação baseada em nome/senha do usuário, os atributos desse elemento são ignorados. Isso inclui `customUserNamePasswordValidatorType`, `includeWindowsGroups`, `membershipProviderName`, e `userNamePasswordValidationMode`.  
  
 Se nenhuma das associações usadas por um serviço estiver configurada para usar autenticação do Windows para o nome de usuário/senha, as configurações relacionadas ao cache de tokens de logon são ignoradas. Isso inclui o `cacheLogonTokenLifetime`, `cacheLogonTokens`, e `maxCacheLogonTokens`.  
  
## <a name="see-also"></a>Consulte também  
 <xref:System.ServiceModel.Configuration.UserNameServiceElement>  
 <xref:System.ServiceModel.Description.ServiceCredentials.UserNameAuthentication%2A>  
 <xref:System.ServiceModel.Security.UserNamePasswordServiceCredential>  
 <xref:System.ServiceModel.Configuration.ServiceCredentialsElement.UserNameAuthentication%2A>
