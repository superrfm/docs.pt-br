---
title: "Níveis de confiança de segurança de acesso a recursos"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: fb5be924-317d-4d69-b33a-3d18ecfb9d6e
caps.latest.revision: "3"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 520a000b11e26b678ad8672bf5d120391434d722
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/22/2017
---
# <a name="security-trust-levels-in-accessing-resources"></a>Níveis de confiança de segurança de acesso a recursos
Este tópico discute como o acesso está restrito a tipos de recursos que <xref:System.Transactions> expõe.  
  
 Há três principais níveis de confiança para <xref:System.Transactions>. Os níveis de confiança são definidos com base nos tipos de recursos que <xref:System.Transactions> expõe e o nível de confiança deve ser necessária para acessar esses recursos. Os recursos que <xref:System.Transactions> fornece acesso a são recursos ampla do sistema, recursos ampla do processo compartilhado e memória do sistema. Os níveis são:  
  
-   **AllowPartiallyTrustedCallers** (APTCA) para aplicativos que usam transações dentro de um único domínio de aplicativo.  
  
-   **DistributedTransactionPermission** (DTP) para aplicativos que usam transações distribuídas.  
  
-   Confiança total para recursos duráveis, aplicativos de gerenciamento de configuração e os aplicativos herdados de interoperabilidade.  
  
> [!NOTE]
>  Você não deve chamar qualquer uma das interfaces de inscrição com contextos representados.  
  
## <a name="trust-levels"></a>Níveis de confiança  
  
### <a name="aptca-partial-trust"></a>APTCA (confiança parcial)  
 O <xref:System.Transactions> assembly pode ser chamado por código parcialmente confiável, porque ela foi marcada com o **AllowPartiallyTrustedCallers** atributo (APTCA). Esse atributo essencialmente remove o implícita <xref:System.Security.Permissions.SecurityAction.LinkDemand> para o **FullTrust** permissão conjunto caso contrário colocado automaticamente em cada método publicamente acessível em cada tipo. No entanto, alguns tipos e membros ainda requerem permissões mais fortes.  
  
 O atributo APTCA permite que aplicativos usem as transações em confiança parcial em um único domínio de aplicativo. Isso permite que as transações não escalonados e inscrições voláteis que podem ser usadas para tratamento de erros. Um exemplo disso é uma tabela de hash transacionado e um aplicativo que utiliza. Dados podem ser adicionados ao e removidos da tabela de hash em uma única transação. Se a transação é posteriormente revertida, todas as alterações feitas na tabela de hash em transação podem ser desfeitas.  
  
### <a name="distributedtransactionpermission-dtp"></a>DistributedTransactionPermission (DTP)  
 Quando um <xref:System.Transactions> transação será escalada para ser gerenciado pelo MSDTC, <xref:System.Transactions> demandas de <xref:System.Transactions.DistributedTransactionPermission> (DTP) para criar a transação distribuída. Isso significa que o código que faz com que a transação ser escalados (como por meio de serialização ou mais inscrições duráveis) precisa ser concedida DTP. O código que criou o <xref:System.Transactions> transação não necessariamente precisa ter essa permissão.  
  
### <a name="fulltrust-link-demands"></a>Demandas de Link FullTrust  
 Esse nível de permissão destina-se para restringir os aplicativos que gravam dados Recursos duráveis. Em caso de falha, o aplicativo precisa ser capaz de recuperar-se com o Gerenciador de transações para determinar o resultado final da transação, para que ele possa atualizar dados permanente. Esse tipo de aplicativo é conhecido como um Gerenciador de fonte durável. Um exemplo clássico desse tipo de aplicativo é SQL.  
  
 Para habilitar a recuperação, esse tipo de aplicativo tem a capacidade de consumir permanentemente os recursos do sistema. Isso ocorre porque o Gerenciador de transações recuperável deve se lembrar de transações que foram confirmadas até que ele possa confirmar que todos os gerenciadores de recursos duráveis que participam da transação tem recebido o resultado. Portanto, esse tipo de aplicativo requer confiança total e não deve ser executado, a menos que nível de confiança recebeu.  
  
 Para obter mais informações sobre inscrições duráveis e recuperação, consulte o [inscrição recursos como participantes em uma transação](../../../../docs/framework/data/transactions/enlisting-resources-as-participants-in-a-transaction.md) e [executar recuperação](../../../../docs/framework/data/transactions/performing-recovery.md) tópicos.  
  
 Aplicativos que executam o trabalho com herdado interoperabilidade com COM+ também precisam ter confiança total.  
  
 A seguir está uma lista de tipos e membros que não podem ser chamados por parcialmente confiável código porque elas são decoradas com o **FullTrust** atributo de segurança declarativa:  
  
 `PermissionSetAttribute(SecurityAction.LinkDemand, Name := "FullTrust")`  
  
-   <xref:System.Transactions.Transaction.EnlistDurable%2A?displayProperty=nameWithType>  
  
-   <xref:System.Transactions.Transaction.EnlistPromotableSinglePhase%2A>  
  
-   <xref:System.Transactions.TransactionInterop>  
  
-   <xref:System.Transactions.TransactionManager.DistributedTransactionStarted>  
  
-   <xref:System.Transactions.HostCurrentTransactionCallback>  
  
-   <xref:System.Transactions.TransactionManager.Reenlist%2A>  
  
-   <xref:System.Transactions.TransactionManager.RecoveryComplete%2A>  
  
-   <xref:System.Transactions.TransactionScope.%23ctor%28System.Transactions.TransactionScopeOption%2CSystem.Transactions.TransactionOptions%2CSystem.Transactions.EnterpriseServicesInteropOption%29>  
  
 Somente o chamador imediato é necessário ter o **FullTrust** conjunto de permissões para usar tipos ou métodos acima.
