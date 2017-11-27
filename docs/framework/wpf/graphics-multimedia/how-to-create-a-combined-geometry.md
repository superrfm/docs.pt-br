---
title: Como criar uma geometria combinada
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-wpf
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- combining geometries [WPF]
- graphics [WPF], combining geometries
- geometries [WPF], combining
ms.assetid: 54c3277c-6b6e-4b25-91be-fda0bbc706b4
caps.latest.revision: "8"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.openlocfilehash: 2be0471f27d26b145cc29847a08bf3bc3b1d51ff
ms.sourcegitcommit: c2e216692ef7576a213ae16af2377cd98d1a67fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/22/2017
---
# <a name="how-to-create-a-combined-geometry"></a>Como criar uma geometria combinada
Este exemplo mostra como combinar geometrias. Para combinar duas geometrias, use um <xref:System.Windows.Media.CombinedGeometry> objeto. Definir seu <xref:System.Windows.Media.CombinedGeometry.Geometry1%2A> e <xref:System.Windows.Media.CombinedGeometry.Geometry2%2A> propriedades com as duas geometrias para combinar e definir o <xref:System.Windows.Media.CombinedGeometry.GeometryCombineMode%2A> propriedade, que determina como as geometrias serão combinadas em conjunto, para `Union`, `Intersect`, `Exclude`, ou `Xor`.  
  
 Para criar uma geometria composta de duas ou mais geometrias, use um <xref:System.Windows.Media.GeometryGroup>.  
  
## <a name="example"></a>Exemplo  
 No exemplo a seguir, uma <xref:System.Windows.Media.CombinedGeometry> está definida com um modo de combinação de geometria de `Exclude`.  Ambos <xref:System.Windows.Media.CombinedGeometry.Geometry1%2A> e <xref:System.Windows.Media.CombinedGeometry.Geometry2%2A> são definidos como círculos de mesmo raio, mas com centros de deslocamento por 50.  
  
 [!code-xaml[GeometrySample#21](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GeometrySample/CS/combininggeometriesexample.xaml#21)]  
  
 ![Resultados da Excluir modo de combinação](../../../../docs/framework/wpf/graphics-multimedia/media/mil-task-combined-geometry-exclude.PNG "mil_task_combined_geometry_exclude")  
Geometria combinada Exclude  
  
 Na marcação a seguir, uma <xref:System.Windows.Media.CombinedGeometry> está definida com um modo combinar de `Intersect`.  Ambos <xref:System.Windows.Media.CombinedGeometry.Geometry1%2A> e <xref:System.Windows.Media.CombinedGeometry.Geometry2%2A> são definidos como círculos de mesmo raio, mas com centros de deslocamento por 50.  
  
 [!code-xaml[GeometrySample#22](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GeometrySample/CS/combininggeometriesexample.xaml#22)]  
  
 ![Resultados da interseção combinam modo](../../../../docs/framework/wpf/graphics-multimedia/media/mil-task-combined-geometry-intersect.PNG "mil_task_combined_geometry_intersect")  
Geometria combinada Intersect  
  
 Na marcação a seguir, uma <xref:System.Windows.Media.CombinedGeometry> está definida com um modo combinar de `Union`.  Ambos <xref:System.Windows.Media.CombinedGeometry.Geometry1%2A> e <xref:System.Windows.Media.CombinedGeometry.Geometry2%2A> são definidos como círculos de mesmo raio, mas com centros de deslocamento por 50.  
  
 [!code-xaml[GeometrySample#23](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GeometrySample/CS/combininggeometriesexample.xaml#23)]  
  
 ![Resultados do modo de combinar de União](../../../../docs/framework/wpf/graphics-multimedia/media/mil-task-combined-geometry-union.PNG "mil_task_combined_geometry_union")  
União de geometria combinada  
  
 Na marcação a seguir, uma <xref:System.Windows.Media.CombinedGeometry> está definida com um modo combinar de `Xor`.  Ambos <xref:System.Windows.Media.CombinedGeometry.Geometry1%2A> e <xref:System.Windows.Media.CombinedGeometry.Geometry2%2A> são definidos como círculos de mesmo raio, mas com centros de deslocamento por 50.  
  
 [!code-xaml[GeometrySample#24](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GeometrySample/CS/combininggeometriesexample.xaml#24)]  
  
 ![Resultados do modo de combinar de Xor](../../../../docs/framework/wpf/graphics-multimedia/media/mil-task-combined-geometry-xor.PNG "mil_task_combined_geometry_xor")  
Geometria combinada Xor