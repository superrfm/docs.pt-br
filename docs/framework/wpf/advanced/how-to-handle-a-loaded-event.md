---
title: Como identificar um evento carregado
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-wpf
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- csharp
- vb
helpviewer_keywords:
- XAML [WPF], Loaded events
- events [WPF], Loaded
- Loaded events [WPF]
ms.assetid: 0cf8d003-8441-4df4-807a-6db09347e829
caps.latest.revision: "12"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 794de0e64e2f4d974091b92f211d7472d04ecd26
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/22/2017
---
# <a name="how-to-handle-a-loaded-event"></a>Como identificar um evento carregado
Este exemplo mostra como tratar o <xref:System.Windows.FrameworkElement.Loaded?displayProperty=nameWithType> evento e um cenário apropriado para o tratamento desse evento. O manipulador cria um <xref:System.Windows.Controls.Button> quando a página for carregada.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir usa [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] junto com um arquivo code-behind.  
  
 [!code-xaml[FELoaded#XAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FELoaded/CSharp/default.xaml#xaml)]  
  
 [!code-csharp[FELoaded#Handler](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FELoaded/CSharp/default.xaml.cs#handler)]
 [!code-vb[FELoaded#Handler](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/FELoaded/VisualBasic/default.xaml.vb#handler)]  
  
## <a name="see-also"></a>Consulte também  
 <xref:System.Windows.FrameworkElement>  
 [Eventos de tempo de vida do objeto](../../../../docs/framework/wpf/advanced/object-lifetime-events.md)  
 [Visão geral de eventos roteados](../../../../docs/framework/wpf/advanced/routed-events-overview.md)  
 [Tópicos de instruções](../../../../docs/framework/wpf/advanced/base-elements-how-to-topics.md)
