---
title: "Como manipular uma exceção usando try-catch (Guia de programação em C#)"
ms.date: 07/20/2015
ms.prod: .net
ms.technology: devlang-csharp
ms.topic: article
helpviewer_keywords:
- exception handling [C#], try/catch blocks
- exceptions [C#], try/catch blocks
- try/catch blocks [C#]
ms.assetid: ca8e3773-980e-4767-8633-7408540e9818
caps.latest.revision: "14"
author: BillWagner
ms.author: wiwagn
ms.openlocfilehash: 9098bbcf5cefb85211f9d3bb9cac15943ba02172
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="how-to-handle-an-exception-using-trycatch-c-programming-guide"></a>Como manipular uma exceção usando try/catch (Guia de Programação em C#)
A finalidade de um bloco [try-catch](../../../csharp/language-reference/keywords/try-catch.md) é capturar e manipular uma exceção gerada pelo código de trabalho. Algumas exceções podem ser manipuladas em um bloco `catch` e o problema pode ser resolvido sem que a exceção seja gerada novamente. No entanto, com mais frequência, a única coisa que você pode fazer é certificar-se de que a exceção apropriada seja gerada.  
  
## <a name="example"></a>Exemplo  
 Neste exemplo, <xref:System.IndexOutOfRangeException> não é a exceção mais apropriada: <xref:System.ArgumentOutOfRangeException> faz mais sentido para o método porque o erro é causado pelo argumento `index` passado pelo chamador.  
  
 [!code-csharp[csProgGuideExceptions#5](../../../csharp/programming-guide/exceptions/codesnippet/CSharp/how-to-handle-an-exception-using-try-catch_1.cs)]  
  
## <a name="comments"></a>Comentários  
 O código que causa uma exceção fica dentro do bloco `try`. A instrução `catch` é adicionada logo após para manipular `IndexOutOfRangeException`, se ocorrer. O bloco `catch` manipula o `IndexOutOfRangeException` e gera a exceção `ArgumentOutOfRangeException`, que é mais adequada. Para fornecer ao chamador tantas informações quanto possível, considere especificar a exceção original como o <xref:System.Exception.InnerException%2A> da nova exceção. Uma vez que a propriedade <xref:System.Exception.InnerException%2A> é [readonly](../../../csharp/language-reference/keywords/readonly.md), você precisa atribuí-la no construtor da nova exceção.  
  
## <a name="see-also"></a>Consulte também  
 [Guia de Programação em C#](../../../csharp/programming-guide/index.md)  
 [Exceções e manipulação de exceções](../../../csharp/programming-guide/exceptions/index.md)  
 [Tratamento de Exceção](../../../csharp/programming-guide/exceptions/exception-handling.md)
