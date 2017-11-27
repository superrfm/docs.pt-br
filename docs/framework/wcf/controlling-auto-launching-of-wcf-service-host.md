---
title: "Controlando a auto inicialização do host de serviço do WCF"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: WcfOptions
ms.assetid: 6abe5d34-519b-4cef-8f02-3c0a7f125585
caps.latest.revision: "8"
author: Erikre
ms.author: erikre
manager: erikre
ms.openlocfilehash: dc89ed3ae41471af49fc92f31834f0ae268309dd
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/18/2017
---
# <a name="controlling-auto-launching-of-wcf-service-host"></a>Controlando a auto inicialização do host de serviço do WCF
Você pode controlar a capacidade de inicialização automática do [!INCLUDE[indigo1](../../../includes/indigo1-md.md)] (WcfSvcHost.exe) de Host de serviço para um [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] projeto de biblioteca de serviço, ao depurar outro projeto na mesma [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] solução que contém vários projetos.  
  
 Para fazer isso, clique com botão direito do [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] projeto de serviço no **Solution Explorer**, escolha **propriedades**e clique em **WCF opções** guia. O **iniciar ao depurar outro projeto na mesma solução o Host de serviço de WCF** caixa de seleção é habilitada por padrão. Você pode desmarcar a caixa de forma que [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] Host de serviço para este projeto específico não é iniciado quando o outro projeto é depurado na mesma solução.  
  
 Esse comportamento não afeta a depuração F5 ou funcionalidades adicionar referência de serviço para este projeto.  
  
 Essa opção está disponível para os projetos a seguir:  
  
-   [!INCLUDE[indigo2](../../../includes/indigo2-md.md)]Projeto de biblioteca de serviço.  
  
-   Projeto de biblioteca de serviço de fluxo de trabalho sequencial.  
  
-   Projeto de biblioteca de serviço de fluxo de trabalho de máquina de estado.  
  
-   Projeto de biblioteca de serviço de distribuição.  
  
## <a name="see-also"></a>Consulte também  
 [WCF Service Host (WcfSvcHost.exe)](../../../docs/framework/wcf/wcf-service-host-wcfsvchost-exe.md) [Host de serviço do WCF (WcfSvcHost.exe)]