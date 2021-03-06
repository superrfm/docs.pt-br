---
title: "Compilação e reutilização em expressões regulares"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-standard
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- parsing text with regular expressions, compilation
- searching with regular expressions, compilation
- .NET Framework regular expressions, engines
- .NET Framework regular expressions, compilation
- regular expressions, compilation
- compilation, regular expressions
- pattern-matching with regular expressions, compilation
- regular expressions, engines
ms.assetid: 182ec76d-5a01-4d73-996c-0b0d14fcea18
caps.latest.revision: "11"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.openlocfilehash: 76acdf2d0d2f7805ec78ea44136bfc63441b9bc9
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/18/2017
---
# <a name="compilation-and-reuse-in-regular-expressions"></a>Compilação e reutilização em expressões regulares
Você pode otimizar o desempenho de aplicativos que fazem uso intensivo de expressões regulares compreendendo como o mecanismo de expressões regulares compila expressões e como as expressões regulares são armazenadas em cache. Este tópico discute a compilação e o cache.  
  
## <a name="compiled-regular-expressions"></a>Expressões regulares compiladas  
 Por padrão, o mecanismo de expressões regulares compila uma expressão regular para uma sequência de instruções internas (esses são códigos de alto nível que são diferentes da Microsoft Intermediate Language ou MSIL). Quando o mecanismo executa uma expressão regular, ele interpreta os códigos internos.  
  
 Se um <xref:System.Text.RegularExpressions.Regex> objeto for construído com o <xref:System.Text.RegularExpressions.RegexOptions.Compiled?displayProperty=nameWithType> opção, ele compila a expressão regular ao código explícito MSIL em vez de instruções internas de expressão regular de alto nível. Isso permite que o compilador JIT (just-in-time) do .NET converta a expressão para um código de computador nativo para um melhor desempenho.  
  
No entanto, a MSIL gerada não pode ser descarregada. A única maneira de descarregar o código é descarregar todo o domínio de aplicativo (ou seja, descarregar todo o código do aplicativo). Efetivamente, uma vez que uma expressão regular é compilada com o <xref:System.Text.RegularExpressions.RegexOptions.Compiled?displayProperty=nameWithType> opção, nunca os libera os recursos usados pela expressão compilada, mesmo se a expressão regular foi criada por uma <xref:System.Text.RegularExpressions.Regex> objeto é liberado para coleta de lixo.  
  
 Você deve ter cuidado para limitar o número de expressões regulares diferentes que você compila com a <xref:System.Text.RegularExpressions.RegexOptions.Compiled?displayProperty=nameWithType> opção para evitar que consuma muitos recursos. Se um aplicativo precisar usar um número grande ou ilimitado de expressões regulares, cada expressão deve ser interpretada, não compilada. No entanto, se um número pequeno de expressões regulares forem usado repetidamente, devem ser compiladas com <xref:System.Text.RegularExpressions.RegexOptions.Compiled?displayProperty=nameWithType> para melhorar o desempenho. Uma alternativa é usar expressões regulares pré-compilados. Você pode compilar todas as suas expressões em uma DLL reutilizável, usando o <xref:System.Text.RegularExpressions.Regex.CompileToAssembly%2A> método. Isso evita a necessidade de compilar no tempo de execução enquanto ainda se beneficia da velocidade de expressões regulares compiladas.  
  
## <a name="the-regular-expressions-cache"></a>Cache de expressões regulares  
 Para melhorar o desempenho, o mecanismo de expressões regulares mantém um cache em todo o aplicativo com as expressões regulares compiladas. O cache armazena padrões de expressões regulares que são usados somente em chamadas de método estático. (Padrões de expressão regular fornecidos para métodos de instância não são armazenados). Isso evita a necessidade de analisar novamente uma expressão em código de bytes de alto nível cada vez que ela for usada.  
  
 O número máximo de expressões regulares em cache é determinado pelo valor da `static` (`Shared` no Visual Basic) <xref:System.Text.RegularExpressions.Regex.CacheSize%2A?displayProperty=nameWithType> propriedade. Por padrão, o mecanismo de expressões regulares armazena em cache até 15 expressões regulares compiladas. Se o número de expressões regulares compiladas ultrapassar o tamanho do cache, a expressão regular menos utilizada recentemente será descartada e a nova expressão regular será armazenada em cache.  
  
 Seu aplicativo pode tirar proveito de expressões regulares pré-compiladas de uma das duas maneiras a seguir:  
  
-   Usando um método estático do <xref:System.Text.RegularExpressions.Regex> objeto para definir a expressão regular. Se você estiver usando um padrão de expressão regular que já foi definido em outra chamada de método estático, o mecanismo de expressões regulares o recuperará do cache. Caso contrário, o mecanismo compilará a expressão regular e a adicionará ao cache.  
  
-   Reutilizando um <xref:System.Text.RegularExpressions.Regex> objeto como o padrão de expressão regular é necessário.  
  
 Devido à sobrecarga de instanciação do objeto e da compilação da expressão regular, criar e destruir rapidamente vários <xref:System.Text.RegularExpressions.Regex> objetos é um processo muito caro. Para aplicativos que usam um grande número de expressões regulares diferentes, você pode otimizar o desempenho por meio de chamadas para estático `Regex` métodos e possivelmente aumentar o tamanho do cache de expressão regular.  
  
## <a name="see-also"></a>Consulte também  
 [Expressões regulares do .NET](../../../docs/standard/base-types/regular-expressions.md)
