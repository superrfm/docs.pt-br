---
title: "Extensão de marcação ColorConvertedBitmap"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-wpf
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- XAML [WPF], ColorConvertedBitmap markup extension
- ColorConvertedBitmap markup extension [WPF]
ms.assetid: 18321c18-c898-4470-93fa-a702b47770c1
caps.latest.revision: "8"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.openlocfilehash: 4f1946ec2a5b607d9fce350da0676092d6e0407a
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="colorconvertedbitmap-markup-extension"></a>Extensão de marcação ColorConvertedBitmap
Fornece uma maneira de especificar uma fonte de bitmap que não tenha um perfil inserido. Contextos de cores / perfis são especificados por [!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)], pois é a origem da imagem [!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)].  
  
## <a name="xaml-attribute-usage"></a>Uso do Atributo XAML  
  
```xml  
<object property="{ColorConvertedBitmap imageSource sourceIIC destinationIIC}" .../>  
```  
  
## <a name="xaml-values"></a>Valores XAML  
  
|||  
|-|-|  
|`imageSource`|O [!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)] de bitmap sem perfil.|  
|`sourceIIC`|O [!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)] da configuração de perfil do código-fonte.|  
|`destinationIIC`|O [!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)] da configuração de perfil de destino|  
  
## <a name="remarks"></a>Comentários  
 Esta extensão de marcação destina-se para preencher um conjunto relacionado de valores de propriedade de origem da imagem, como <xref:System.Windows.Media.Imaging.BitmapImage.UriSource%2A>.  
  
 A sintaxe de atributo é a sintaxe mais comum usada com essa extensão de marcação. `ColorConvertedBitmap`(ou `ColorConvertedBitmapExtension`) não pode ser usado na sintaxe de elemento de propriedade, porque os valores só podem ser definidos como valores no construtor inicial, que é a cadeia de caracteres após o identificador da extensão.  
  
 `ColorConvertedBitmap` é uma extensão da marcação. Extensões de marcação são tipicamente implementadas quando existe um requisito que permite que valores de atributo sejam diferentes de valores literais ou nomes de manipuladores, e o requisito é mais global do que simplesmente colocar conversores de tipo em certos tipos ou propriedades. Todas as extensões de marcação em [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] usam os caracteres { e } na sintaxe de atributo, que é a convenção pela qual um processador [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] reconhece que uma extensão de marcação deve processar o atributo. Para obter mais informações, consulte [Extensões de marcação e XAML do WPF](../../../../docs/framework/wpf/advanced/markup-extensions-and-wpf-xaml.md).  
  
## <a name="see-also"></a>Consulte também  
 <xref:System.Windows.Media.Imaging.BitmapImage.UriSource%2A>  
 [Extensões de marcação e XAML WPF](../../../../docs/framework/wpf/advanced/markup-extensions-and-wpf-xaml.md)  
 [Visão geral da geração de imagens](../../../../docs/framework/wpf/graphics-multimedia/imaging-overview.md)