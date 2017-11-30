---
title: "APIs de suporte à hospedagem de navegador do WPF nativa"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-wpf
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: AutoGeneratedOrientationPage
helpviewer_keywords:
- browser hosting support [WPF]
- WPF browser hosting support APIs [WPF]
ms.assetid: 82c133a8-d760-45fb-a2b9-3a997537f1d4
caps.latest.revision: "33"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.openlocfilehash: ff548f490d76215305d2e22878bc35a54e3bd009
ms.sourcegitcommit: c2e216692ef7576a213ae16af2377cd98d1a67fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/22/2017
---
# <a name="native-wpf-browser-hosting-support-apis"></a>APIs de suporte à hospedagem de navegador do WPF nativa
A hospedagem de aplicações [!INCLUDE[TLA#tla_titlewinclient](../../../../includes/tlasharptla-titlewinclient-md.md)] em navegadores da Web é facilitada por um servidor de documento ativo (também conhecido como DocObject) registrado no host WPF. [!INCLUDE[TLA2#tla_ie](../../../../includes/tla2sharptla-ie-md.md)] pode ativar e integrar diretamente com um documento ativo. Para hospedar documentos XBAPs e XAML Flexível em navegadores Mozilla, [!INCLUDE[TLA#tla_titlewinclient](../../../../includes/tlasharptla-titlewinclient-md.md)] fornece um plug-in NPAPI, que oferece um ambiente de hospedagem semelhante ao [!INCLUDE[TLA#tla_titlewinclient](../../../../includes/tlasharptla-titlewinclient-md.md)] servidor de documento ativo como faz o [!INCLUDE[TLA2#tla_ie](../../../../includes/tla2sharptla-ie-md.md)]. Entretanto, a maneira mais fácil de hospedar documentos XBAPs e XAML em outros navegadores e aplicativos independentes é através do controle do navegador da Web do Internet Explorer. O controle do Navegador da Web fornece o complexo ambiente de hospedagem do servidor de documento ativo, mas permite que seu próprio host personalize e amplie esse ambiente e se comunique diretamente com o servidor de documento ativo atual.  
  
 O [!INCLUDE[TLA#tla_titlewinclient](../../../../includes/tlasharptla-titlewinclient-md.md)] servidor de documento ativo implementa várias interfaces de hospedagem comuns, incluindo [IOleObject](http://go.microsoft.com/fwlink/?LinkId=162049), [IOleDocument](http://go.microsoft.com/fwlink/?LinkId=162050), [IOleInPlaceActiveObject](http://go.microsoft.com/fwlink/?LinkId=162051), [IPersistMoniker](http://go.microsoft.com/fwlink/?LinkId=162045), [IOleCommandTarget](http://go.microsoft.com/fwlink/?LinkId=162047). Quando hospedada no controle do navegador da Web, essas interfaces podem ser consultas do objeto retornadas pela propriedade [IWebBrowser2::Document](http://go.microsoft.com/fwlink/?LinkId=162048).  
  
## <a name="iolecommandtarget"></a>IOleCommandTarget  
 A implementação do [IOleCommandTarget](http://go.microsoft.com/fwlink/?LinkId=162047) do servidor de documento ativo do WPF dá suporte a vários comandos relacionados à navegação e ao navegador do grupo de comandos OLE padrão (com um GUID de grupo de comandos nulo). Além disso, reconhece um grupo de comando personalizado chamado CGID_PresentationHost. Atualmente, só há um comando definido neste grupo.  
  
```  
DEFINE_GUID(CGID_PresentationHost, 0xd0288c55, 0xd6, 0x4f5e, 0xa8, 0x51, 0x79, 0xde, 0xc5, 0x1b, 0x10, 0xec);  
enum PresentationHostCommands {   
   PHCMDID_TABINTO = 1   
};  
```  
  
 PHCMDID_TABINTO instrui o PresentationHost a mudar o foco para o primeiro ou último elemento que pode ser focado em seu conteúdo, dependendo do estado da tecla Shift.  
  
## <a name="in-this-section"></a>Nesta seção  
 [IEnumRAWINPUTDEVICE](../../../../docs/framework/wpf/app-development/ienumrawinputdevice.md)  
 [IWpfHostSupport](../../../../docs/framework/wpf/app-development/iwpfhostsupport.md)