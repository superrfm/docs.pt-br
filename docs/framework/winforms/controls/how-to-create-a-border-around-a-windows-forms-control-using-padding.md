---
title: Como criar uma borda em torno de um controle dos Windows Forms usando preenchimento
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-winforms
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- csharp
- vb
helpviewer_keywords:
- margins
- controls [Windows Forms], Margin property
- padding [Windows Forms], Windows Forms
- controls [Windows Forms], Padding property
- controls [Windows Forms], outlining
- Padding property [Windows Forms]
- margins [Windows Forms], Windows Forms
- Margin property [Windows Forms]
ms.assetid: bac7ed4d-a163-4259-98bd-155a36345890
caps.latest.revision: "5"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 7b8fc8774e1f861db989b05678235ea34e38318c
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/22/2017
---
# <a name="how-to-create-a-border-around-a-windows-forms-control-using-padding"></a>Como criar uma borda em torno de um controle dos Windows Forms usando preenchimento
O exemplo de código a seguir demonstra como criar uma borda ou estrutura de tópicos ao redor de um <xref:System.Windows.Forms.RichTextBox> controle. O exemplo define o valor de um <xref:System.Windows.Forms.Panel> do controle <xref:System.Windows.Forms.Padding> propriedade como 5 e define o <xref:System.Windows.Forms.Control.Dock%2A> propriedade de um filho <xref:System.Windows.Forms.RichTextBox> controle <xref:System.Windows.Forms.DockStyle.Fill>. O <xref:System.Windows.Forms.Control.BackColor%2A> do <xref:System.Windows.Forms.Panel> controle é definido como <xref:System.Drawing.Color.Blue%2A>, que cria uma borda azul ao redor de <xref:System.Windows.Forms.RichTextBox> controle.  
  
## <a name="example"></a>Exemplo  
 [!code-csharp[System.Windows.Forms.Padding#1](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Padding/CS/Form1.cs#1)]
 [!code-vb[System.Windows.Forms.Padding#1](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Padding/VB/Form1.vb#1)]  
  
## <a name="see-also"></a>Consulte também  
 <xref:System.Windows.Forms.Padding>  
 [Margem e preenchimento em controles dos Windows Forms](../../../../docs/framework/winforms/controls/margin-and-padding-in-windows-forms-controls.md)
