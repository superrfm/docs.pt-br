---
title: "Operador ^ (Referência de C#)"
ms.date: 07/20/2015
ms.prod: .net
ms.technology: devlang-csharp
ms.topic: article
f1_keywords: ^_CSharpKeyword
helpviewer_keywords:
- ^ operator [C#]
- bitwise exclusive OR operator [C#]
ms.assetid: b09bc815-570f-4db6-a637-5b4ed99d014a
caps.latest.revision: "19"
author: BillWagner
ms.author: wiwagn
ms.openlocfilehash: 4ccd32ea8abd8ca3252380083eafecad2b572ed7
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="-operator-c-reference"></a>Operador ^ (Referência de C#)
Os operadores binários `^` são predefinidos para os tipos integrais e `bool`. Para os tipos integrais, o `^` computa o OR exclusivo bit a bit de seus operandos. Para operandos `bool`, o `^` computa o OR exclusivo lógico de seus operandos; ou seja, o resultado será `true` se e somente se exatamente um dos operandos for `true`.  
  
## <a name="remarks"></a>Comentários  
 Os tipos definidos pelo usuário podem sobrecarregar o operador `^` (consulte [operador](../../../csharp/language-reference/keywords/operator.md)). As operações em tipos integrais geralmente são permitidas na enumeração.  
  
## <a name="example"></a>Exemplo  
 [!code-csharp[csRefOperators#30](../../../csharp/language-reference/operators/codesnippet/CSharp/xor-operator_1.cs)]  
  
 O cálculo de `0xf8 ^ 0x3f` no exemplo anterior executa um OR exclusivo bit a bit dos dois valores binários a seguir, que correspondem aos valores hexadecimais F8 e 3F:  
  
 `1111 1000`  
  
 `0011 1111`  
  
 O resultado do OR exclusivo é `1100 0111`, que é igual a C7 em hexadecimal.  
  
## <a name="see-also"></a>Consulte também  
 [Referência de C#](../../../csharp/language-reference/index.md)  
 [Guia de Programação em C#](../../../csharp/programming-guide/index.md)  
 [Operadores do C#](../../../csharp/language-reference/operators/index.md)
