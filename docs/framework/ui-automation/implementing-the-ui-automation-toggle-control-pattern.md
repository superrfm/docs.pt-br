---
title: "Implementando o padrão de controle Toggle de automação de interface de usuário"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-bcl
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Toggle control pattern
- control patterns, Toggle
- UI Automation, Toggle control pattern
ms.assetid: 3cfe875f-b0c0-413d-9703-5f14e6a1a30e
caps.latest.revision: "19"
author: Xansky
ms.author: mhopkins
manager: markl
ms.workload: dotnet
ms.openlocfilehash: 73a1182adad742f1cb53b809ae07d78d1ec27cd9
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/22/2017
---
# <a name="implementing-the-ui-automation-toggle-control-pattern"></a>Implementando o padrão de controle Toggle de automação de interface de usuário
> [!NOTE]
>  Esta documentação destina-se a desenvolvedores do .NET Framework que querem usar as classes da [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] gerenciadas definidas no namespace <xref:System.Windows.Automation>. Para obter as informações mais recentes sobre a [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], consulte [Windows Automation API: UI Automation](http://go.microsoft.com/fwlink/?LinkID=156746) (API de Automação do Windows: Automação da Interface do Usuário).  
  
 Este tópico apresenta diretrizes e convenções para implementar <xref:System.Windows.Automation.Provider.IToggleProvider>, incluindo informações sobre os métodos e propriedades. Links para referências adicionais são listadas no final do tópico.  
  
 O <xref:System.Windows.Automation.TogglePattern> padrão de controle é usado para oferecer suporte aos controles que podem alternar entre um conjunto de estados e manter um estado definido uma vez. Para obter exemplos de controles que implementam este padrão de controle, consulte [mapeamento de padrão de controle para clientes de automação de interface do usuário](../../../docs/framework/ui-automation/control-pattern-mapping-for-ui-automation-clients.md).  
  
<a name="Implementation_Guidelines_and_Conventions"></a>   
## <a name="implementation-guidelines-and-conventions"></a>Convenções e diretrizes de implementação  
 Ao implementar o padrão de controle Toggle, observe as seguintes diretrizes e convenções:  
  
-   Controles que não mantêm o estado quando ativado, como botões, botões da barra de ferramentas e hiperlinks, devem implementar <xref:System.Windows.Automation.Provider.IInvokeProvider> em vez disso.  
  
-   Um controle deve percorrer seu <xref:System.Windows.Automation.ToggleState> na seguinte ordem: <xref:System.Windows.Automation.ToggleState.On>, <xref:System.Windows.Automation.ToggleState.Off> e, se suportado, <xref:System.Windows.Automation.ToggleState.Indeterminate>.  
  
-   <xref:System.Windows.Automation.TogglePattern>não fornece um método SetState devido a problemas envolvendo a configuração direta de uma caixa de seleção de três estados sem percorrer seu apropriado <xref:System.Windows.Automation.ToggleState> sequência.  
  
-   O controle RadioButton não implementa <xref:System.Windows.Automation.Provider.IToggleProvider>, pois não é capaz de percorrendo seus estados válidos.  
  
<a name="Required_Members_for_IToggleProvider"></a>   
## <a name="required-members-for-itoggleprovider"></a>Membros necessários para IToggleProvider  
 As propriedades e métodos a seguir são necessários para implementar <xref:System.Windows.Automation.Provider.IToggleProvider>.  
  
|Membro necessário|Tipo de membro|Observações|  
|---------------------|-----------------|-----------|  
|<xref:System.Windows.Automation.TogglePattern.Toggle%2A>|Método|Nenhum|  
|<xref:System.Windows.Automation.TogglePatternIdentifiers.ToggleStateProperty>|Propriedade|Nenhum|  
  
 Esse padrão de controle não possui eventos associados.  
  
<a name="Exceptions"></a>   
## <a name="exceptions"></a>Exceções  
 Esse padrão de controle não tem exceção associada.  
  
## <a name="see-also"></a>Consulte também  
 [Visão geral de padrões de controle de automação da interface do usuário](../../../docs/framework/ui-automation/ui-automation-control-patterns-overview.md)  
 [Suporte a padrões de controle em um provedor de automação de interface do usuário](../../../docs/framework/ui-automation/support-control-patterns-in-a-ui-automation-provider.md)  
 [Padrões de controle de automação de interface do usuário para clientes](../../../docs/framework/ui-automation/ui-automation-control-patterns-for-clients.md)  
 [Obter o estado de Alternância de uma caixa de seleção usando automação de interface do usuário](../../../docs/framework/ui-automation/get-the-toggle-state-of-a-check-box-using-ui-automation.md)  
 [Visão geral de árvore de automação de interface do usuário](../../../docs/framework/ui-automation/ui-automation-tree-overview.md)  
 [Usar o cache em automação de interface do usuário](../../../docs/framework/ui-automation/use-caching-in-ui-automation.md)
