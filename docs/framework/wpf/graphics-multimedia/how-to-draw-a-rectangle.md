---
title: "Como desenhar um retângulo"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-wpf
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- drawing [WPF], rectangles
- graphics [WPF], rectangles
- rectangles [WPF], drawing
ms.assetid: beeb57ef-fab5-4446-a38a-1588f97b4c2f
caps.latest.revision: "10"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 58f29783e48aa7173010ffec6a65f9ac1d8a2b62
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/22/2017
---
# <a name="how-to-draw-a-rectangle"></a>Como desenhar um retângulo
Este exemplo mostra como desenhar um retângulo, usando o <xref:System.Windows.Shapes.Rectangle> elemento.  
  
 Para desenhar um retângulo, crie um <xref:System.Windows.Shapes.Rectangle> elemento e especifique seu <xref:System.Windows.FrameworkElement.Width%2A> e <xref:System.Windows.FrameworkElement.Height%2A>. Para pintar o interior de um retângulo, defina seu <xref:System.Windows.Shapes.Shape.Fill%2A>. Para fornecer uma estrutura de tópicos de retângulo, use seu <xref:System.Windows.Shapes.Shape.Stroke%2A> e <xref:System.Windows.Shapes.Shape.StrokeThickness%2A> propriedades.  
  
 Para dar o retângulo arredondado cantos, especifique o valor opcional <xref:System.Windows.Shapes.Rectangle.RadiusX%2A> e <xref:System.Windows.Shapes.Rectangle.RadiusY%2A> propriedades. O <xref:System.Windows.Shapes.Rectangle.RadiusX%2A> e <xref:System.Windows.Shapes.Rectangle.RadiusY%2A> propriedades definem o raios eixos x e y da elipse que é usada para arredondar os cantos do retângulo.  
  
 No exemplo a seguir, dois <xref:System.Windows.Shapes.Rectangle> elementos são desenhados em um <xref:System.Windows.Controls.Canvas>. O primeiro retângulo tem um <xref:System.Windows.Media.Brushes.Blue%2A> interiores. O segundo retângulo tem um <xref:System.Windows.Media.Brushes.Blue%2A> interiores, uma <xref:System.Windows.Media.Brushes.Black%2A> contorno e cantos arredondados.  
  
## <a name="example"></a>Exemplo  
 [!code-xaml[drawingwithshapeelements#Rectangle1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DrawingWithShapeElements/CS/rectangleexample.xaml#rectangle1)]  
  
 Embora este exemplo usa um <xref:System.Windows.Controls.Canvas> para conter os retângulos, você pode usar elementos de retângulo (e todos os outros elementos de forma) com qualquer <xref:System.Windows.Controls.Panel> ou <xref:System.Windows.Controls.Control> que dá suporte a conteúdo não texto. Na verdade, retângulos são particularmente útil para exibir planos de fundo para as partes <xref:System.Windows.Controls.Grid> painéis. Para ver um exemplo, consulte a [Visão geral da tabela](../../../../docs/framework/wpf/advanced/table-overview.md).  
  
 Este exemplo faz parte de um exemplo maior; para ver o exemplo completo, consulte o [Exemplo de elementos de forma](http://go.microsoft.com/fwlink/?LinkID=160037).  
  
## <a name="see-also"></a>Consulte também  
 <xref:System.Windows.Shapes.Rectangle>  
 [Exemplo de elementos de forma](http://go.microsoft.com/fwlink/?LinkID=160037)  
 [Visão geral de formas e desenho básico no WPF](../../../../docs/framework/wpf/graphics-multimedia/shapes-and-basic-drawing-in-wpf-overview.md)  
 [Visão geral da tabela](../../../../docs/framework/wpf/advanced/table-overview.md)
