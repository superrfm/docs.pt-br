---
title: "Expor um provedor de automação de interface do usuário do lado do servidor"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-bcl
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- csharp
- vb
helpviewer_keywords:
- expose a server-side UI Automation provider
- UI Automation, server-side provider, exposing
- server-side UI Automation provider, exposing
ms.assetid: 55d419c0-2201-4101-90c9-2888df4dbb47
caps.latest.revision: "20"
author: Xansky
ms.author: mhopkins
manager: markl
ms.workload: dotnet
ms.openlocfilehash: b18bf705c0aefcc8d10575b8b4648d2e2bcaccb7
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/22/2017
---
# <a name="expose-a-server-side-ui-automation-provider"></a>Expor um provedor de automação de interface do usuário do lado do servidor
> [!NOTE]
>  Esta documentação destina-se a desenvolvedores do .NET Framework que querem usar as classes da [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] gerenciadas definidas no namespace <xref:System.Windows.Automation>. Para obter as informações mais recentes sobre a [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], consulte [Windows Automation API: UI Automation](http://go.microsoft.com/fwlink/?LinkID=156746) (API de Automação do Windows: Automação da Interface do Usuário).  
  
 Este tópico contém código de exemplo que mostra como expor um provedor de automação de interface do usuário do lado do servidor que está hospedado em um <xref:System.Windows.Forms.Control?displayProperty=nameWithType> janela.  
  
 O exemplo substitui o procedimento de janela para interceptar WM_GETOBJECT, que é a mensagem enviado pelo [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] serviço principal, quando um aplicativo cliente solicita informações sobre a janela.  
  
## <a name="example"></a>Exemplo  
 [!code-csharp[UIAFragmentProvider_snip#116](../../../samples/snippets/csharp/VS_Snippets_Wpf/UIAFragmentProvider_snip/CSharp/ListFragment.cs#116)]
 [!code-vb[UIAFragmentProvider_snip#116](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/UIAFragmentProvider_snip/VisualBasic/ListFragment.vb#116)]  
  
## <a name="see-also"></a>Consulte também  
 [Visão geral dos provedores de automação de interface do usuário](../../../docs/framework/ui-automation/ui-automation-providers-overview.md)  
 [Implementação de provedor de Automação da Interface do Usuário no lado do servidor](../../../docs/framework/ui-automation/server-side-ui-automation-provider-implementation.md)
