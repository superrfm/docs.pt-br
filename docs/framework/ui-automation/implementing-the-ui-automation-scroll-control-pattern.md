---
title: "Implementando o padrão de controle Scroll de automação de interface do usuário"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-bcl
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- UI Automation, Scroll control pattern
- control patterns, Scroll
- Scroll control pattern
ms.assetid: 73d64242-6cbb-424c-92dd-dc69530b7899
caps.latest.revision: "23"
author: Xansky
ms.author: mhopkins
manager: markl
ms.workload: dotnet
ms.openlocfilehash: 9ad069a4670cc7e4c2281109d8df6afa55ea6dea
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/22/2017
---
# <a name="implementing-the-ui-automation-scroll-control-pattern"></a>Implementando o padrão de controle Scroll de automação de interface do usuário
> [!NOTE]
>  Esta documentação destina-se a desenvolvedores do .NET Framework que querem usar as classes da [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] gerenciadas definidas no namespace <xref:System.Windows.Automation>. Para obter as informações mais recentes sobre a [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], consulte [Windows Automation API: UI Automation](http://go.microsoft.com/fwlink/?LinkID=156746) (API de Automação do Windows: Automação da Interface do Usuário).  
  
 Este tópico apresenta diretrizes e convenções para implementar <xref:System.Windows.Automation.Provider.IScrollProvider>, incluindo informações sobre propriedades e eventos. Links para referências adicionais são listadas no final do tópico.  
  
 O <xref:System.Windows.Automation.ScrollPattern> padrão de controle é usado para dar suporte a um controle que atua como um contêiner rolável para uma coleção de objetos filho. O controle não é necessário usar as barras de rolagem para dar suporte à funcionalidade de rolagem, embora normalmente faz.  
  
 ![Controle de rolagem sem barras de rolagem. ] (../../../docs/framework/ui-automation/media/uia-scrollpattern-without-scrollbars.PNG "UIA_ScrollPattern_Without_Scrollbars")  
Exemplo de um controle de rolagem que não usa barras de rolagem  
  
 Para obter exemplos de controles que implementam este controle, consulte [mapeamento de padrão de controle para clientes de automação de interface do usuário](../../../docs/framework/ui-automation/control-pattern-mapping-for-ui-automation-clients.md).  
  
<a name="Implementation_Guidelines_and_Conventions"></a>   
## <a name="implementation-guidelines-and-conventions"></a>Convenções e diretrizes de implementação  
 Ao implementar o padrão de controle Scroll, observe as seguintes diretrizes e convenções:  
  
-   O filho desse controle deve implementar <xref:System.Windows.Automation.Provider.IScrollItemProvider>.  
  
-   As barras de rolagem de um controle de contêiner não dão suporte a <xref:System.Windows.Automation.ScrollPattern> padrão de controle. Eles devem dar suporte a <xref:System.Windows.Automation.RangeValuePattern> em vez disso, o padrão de controle.  
  
-   Quando a rolagem é medido em porcentagens, todos os valores ou valores relacionados à graduação de rolagem deve ser normalizadas em um intervalo de 0 a 100.  
  
-   <xref:System.Windows.Automation.ScrollPatternIdentifiers.HorizontallyScrollableProperty>e <xref:System.Windows.Automation.ScrollPatternIdentifiers.VerticallyScrollableProperty> são independentes de <xref:System.Windows.Automation.AutomationElement.IsEnabledProperty>.  
  
-   Se <xref:System.Windows.Automation.ScrollPatternIdentifiers.HorizontallyScrollableProperty>  =  `false` , em seguida, <xref:System.Windows.Automation.ScrollPatternIdentifiers.HorizontalViewSizeProperty> deve ser definido como 100% e <xref:System.Windows.Automation.ScrollPatternIdentifiers.HorizontalScrollPercentProperty> deve ser definido como <xref:System.Windows.Automation.ScrollPatternIdentifiers.NoScroll>. Da mesma forma, se <xref:System.Windows.Automation.ScrollPatternIdentifiers.VerticallyScrollableProperty>  =  `false` , em seguida, <xref:System.Windows.Automation.ScrollPatternIdentifiers.VerticalViewSizeProperty> deve ser definido como 100 por cento e <xref:System.Windows.Automation.ScrollPatternIdentifiers.VerticalScrollPercentProperty> deve ser definido como <xref:System.Windows.Automation.ScrollPatternIdentifiers.NoScroll>. Isso permite que um cliente de automação de interface do usuário para usar esses valores de propriedade dentro de <xref:System.Windows.Automation.ScrollPattern.SetScrollPercent%2A> método evitando uma [condição de corrida](http://support.microsoft.com/default.aspx?scid=kb;en-us;317723) se uma direção o cliente não estiver interessado em rolagem fica ativado.  
  
-   <xref:System.Windows.Automation.Provider.IScrollProvider.HorizontalScrollPercent%2A>é específico da localidade. Configuração HorizontalScrollPercent = 100,0 deve definir o local de rolagem do controle para o equivalente da sua posição mais à direita para idiomas como o inglês leitura à esquerda para a direita. Como alternativa, para idiomas como árabe em que se lê da direita para esquerda, a configuração HorizontalScrollPercent = 100,0 deve definir o local de rolagem para a esquerda.  
  
<a name="Required_Members_for_IScrollProvider"></a>   
## <a name="required-members-for-iscrollprovider"></a>Membros necessários para IScrollProvider  
 As propriedades e métodos a seguir são necessários para implementar <xref:System.Windows.Automation.Provider.IScrollProvider>.  
  
|Membro necessário|Tipo de membro|Observações|  
|---------------------|-----------------|-----------|  
|<xref:System.Windows.Automation.Provider.IScrollProvider.HorizontalScrollPercent%2A>|Propriedade|Nenhum|  
|<xref:System.Windows.Automation.Provider.IScrollProvider.VerticalScrollPercent%2A>|Propriedade|Nenhum|  
|<xref:System.Windows.Automation.Provider.IScrollProvider.HorizontalViewSize%2A>|Propriedade|Nenhum|  
|<xref:System.Windows.Automation.Provider.IScrollProvider.VerticalViewSize%2A>|Propriedade|Nenhum|  
|<xref:System.Windows.Automation.Provider.IScrollProvider.HorizontallyScrollable%2A>|Propriedade|Nenhum|  
|<xref:System.Windows.Automation.Provider.IScrollProvider.VerticallyScrollable%2A>|Propriedade|Nenhum|  
|<xref:System.Windows.Automation.Provider.IScrollProvider.Scroll%2A>|Método|Nenhum|  
|<xref:System.Windows.Automation.Provider.IScrollProvider.SetScrollPercent%2A>|Método|Nenhum|  
  
 Esse padrão de controle não possui eventos associados.  
  
<a name="Exceptions"></a>   
## <a name="exceptions"></a>Exceções  
 Provedores devem lançar as exceções a seguir.  
  
|Tipo de exceção|Condição|  
|--------------------|---------------|  
|<xref:System.ArgumentException>|<xref:System.Windows.Automation.Provider.IScrollProvider.Scroll%2A>lança esta exceção se um controle suporta <xref:System.Windows.Automation.ScrollAmount.SmallIncrement> valores exclusivamente para rolagem horizontal ou vertical, mas um <xref:System.Windows.Automation.ScrollAmount.LargeIncrement> valor é passado.|  
|<xref:System.ArgumentException>|<xref:System.Windows.Automation.Provider.IScrollProvider.SetScrollPercent%2A>lança esta exceção quando um valor que não pode ser convertido para um double é passado.|  
|<xref:System.ArgumentOutOfRangeException>|<xref:System.Windows.Automation.Provider.IScrollProvider.SetScrollPercent%2A>lança esta exceção quando um valor maior que 100 ou menor que 0 é passado (exceto -1 que é equivalente a <xref:System.Windows.Automation.ScrollPatternIdentifiers.NoScroll>).|  
|<xref:System.InvalidOperationException>|Ambos <xref:System.Windows.Automation.Provider.IScrollProvider.Scroll%2A> e <xref:System.Windows.Automation.Provider.IScrollProvider.SetScrollPercent%2A> lançam essa exceção quando é feita uma tentativa de rolagem em uma direção não suportada.|  
  
## <a name="see-also"></a>Consulte também  
 [Visão geral de padrões de controle de automação da interface do usuário](../../../docs/framework/ui-automation/ui-automation-control-patterns-overview.md)  
 [Suporte a padrões de controle em um provedor de automação de interface do usuário](../../../docs/framework/ui-automation/support-control-patterns-in-a-ui-automation-provider.md)  
 [Padrões de controle de automação de interface do usuário para clientes](../../../docs/framework/ui-automation/ui-automation-control-patterns-for-clients.md)  
 [Visão geral de árvore de automação de interface do usuário](../../../docs/framework/ui-automation/ui-automation-tree-overview.md)  
 [Usar o cache em automação de interface do usuário](../../../docs/framework/ui-automation/use-caching-in-ui-automation.md)
