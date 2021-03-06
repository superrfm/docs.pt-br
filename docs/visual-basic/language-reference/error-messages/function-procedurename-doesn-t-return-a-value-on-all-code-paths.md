---
title: "Função &#39; &lt;procedurename&gt;&#39; &#39; t retorna um valor em todos os caminhos de código"
ms.date: 07/20/2015
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: devlang-visual-basic
ms.topic: article
f1_keywords:
- bc42105
- vbc42105
helpviewer_keywords: BC42105
ms.assetid: b6929bf4-a365-4a70-8dc9-6b0fc09e1468
caps.latest.revision: "12"
author: dotnet-bot
ms.author: dotnetcontent
ms.openlocfilehash: 5244d97a79f2450f44fe05f63510369914375912
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="function-39ltprocedurenamegt39-doesn39t-return-a-value-on-all-code-paths"></a>Função &#39; &lt;procedurename&gt;&#39; &#39; t retorna um valor em todos os caminhos de código
Função '\<procedurename >' não retorna um valor em todos os caminhos de código. Uma instrução 'Return' está faltando?  
  
 Um `Function` procedimento tem pelo menos um caminho possível pelo seu código que não retorna um valor.  
  
 Você pode retornar um valor de uma `Function` procedimento em qualquer uma das seguintes maneiras:  
  
-   Incluir o valor em uma [instrução Return](../../../visual-basic/language-reference/statements/return-statement.md).  
  
-   Atribuir o valor para o `Function` procedimento nome e, em seguida, executar um `Exit Function` instrução.  
  
-   Atribuir o valor para o `Function` procedimento nome e, em seguida, executar o `End Function` instrução.  
  
 Se o controle passará para `Exit Function` ou `End Function` e você não tiver atribuído qualquer valor para o nome do procedimento, o procedimento retorna o valor padrão do tipo de dados de retorno. Para obter mais informações, consulte "Comportamento" em [instrução Function](../../../visual-basic/language-reference/statements/function-statement.md).  
  
 Por padrão, esta mensagem é um aviso. Para obter mais informações sobre como ocultar avisos ou tratar avisos como erros, consulte [Configurando avisos no Visual Basic](/visualstudio/ide/configuring-warnings-in-visual-basic).  
  
 **ID do erro:** BC42105  
  
## <a name="to-correct-this-error"></a>Para corrigir este erro  
  
-   Verifique sua lógica de fluxo de controle e verifique se que você atribuir um valor antes de cada instrução que produz um retorno.  
  
     É mais fácil garantir que cada retorno do procedimento retorna um valor se você usar sempre o `Return` instrução. Se você fizer isso, a última instrução antes de `End Function` deve ser um `Return` instrução.  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos de Função](../../../visual-basic/programming-guide/language-features/procedures/function-procedures.md)  
 [Instrução Function](../../../visual-basic/language-reference/statements/function-statement.md)  
 [Página de Compilação, Designer de Projeto (Visual Basic)](/visualstudio/ide/reference/compile-page-project-designer-visual-basic)
