---
title: Tipo de dados Long (Visual Basic)
ms.date: 01/31/2018
ms.prod: .net
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vb.Long
helpviewer_keywords:
- identifier type characters [Visual Basic], &
- numbers [Visual Basic], whole
- whole numbers
- integral data types [Visual Basic]
- '& identifier type character'
- integer numbers
- literal type characters [Visual Basic], L
- numbers [Visual Basic], integer
- integers [Visual Basic], data types
- L literal type character [Visual Basic]
- integers [Visual Basic], types
- Long keyword [Visual Basic]
- data types [Visual Basic], integral
- data types [Visual Basic], assigning
- Long data type
ms.assetid: b4770c34-1804-4f8c-b512-c10b0893e516
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 51cf03afc6b2e77ccca74fc26365fc50110e1f71
ms.sourcegitcommit: d2da0142247ef42a219a5d2907f153e62dc6ea0d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2018
---
# <a name="long-data-type-visual-basic"></a>Tipo de dados Long (Visual Basic)

Armazena inteiros de 64 bits (8 bytes) cujo valor varia de -9.223.372.036.854.775.808 a 9.223.372.036.854.775.807 (9.2 … E + 18).  
  
## <a name="remarks"></a>Comentários

 Use o `Long` tipo de dados para conter números inteiros que são muito grandes para caber no `Integer` tipo de dados.  
  
 O valor padrão de `Long` é 0.

## <a name="literal-assignments"></a>Atribuições de literal 

Você pode declarar e inicializar uma `Long` variável atribuindo a ele um literal decimal, hexadecimal literal, um literal octal, ou (começando com Visual Basic 2017) um literal binário. Se o literal inteiro estiver fora do intervalo de `Long` (ou seja, se for menor que <xref:System.Int64.MinValue?displayProperty=nameWithType> ou maior que <xref:System.Int64.MaxValue?displayProperty=nameWithType>, ocorrerá um erro de compilação.

No exemplo a seguir, inteiros iguais a 4.294.967.296 representados como literais decimais, hexadecimais e binários são atribuídos a valores `Long`.
  
[!code-vb[long](../../../../samples/snippets/visualbasic/language-reference/data-types/numeric-literals.vb#Long)]  

> [!NOTE]
> Use o prefixo `&h` ou `&H` para denotar um hexadecimal literal, o prefixo `&b` ou `&B` para denotar um literal binário e o prefixo `&o` ou `&O` para denotar um literal octal. Literais decimais não têm nenhum prefixo.

A partir do Visual Basic de 2017, você também pode usar o caractere de sublinhado, `_`, como um separador de dígito para melhorar a legibilidade, como o exemplo a seguir mostra.

[!code-vb[long](../../../../samples/snippets/visualbasic/language-reference/data-types/numeric-literals.vb#LongS)]

A partir do Visual Basic 15,5, você também pode usar o caractere de sublinhado (`_`) como um separador à esquerda entre o prefixo e os dígitos hexadecimais, binários ou octais. Por exemplo:

```vb
Dim number As Long = &H_0FAC_0326_1489_D68C
```

[!INCLUDE [supporting-underscores](../../../../includes/vb-separator-langversion.md)]

Literais numéricos também podem incluir o `L` [caractere de tipo](../../programming-guide\language-features\data-types/type-characters.md) para denotar o `Long` tipo de dados, como mostra o exemplo a seguir.

```vb
Dim number = &H_0FAC_0326_1489_D68CL
```

## <a name="programming-tips"></a>Dicas de programação

-   **Considerações de interoperabilidade.** Se você estiver fazendo interface com componentes não escritos para o .NET Framework, como objetos de automação ou COM, lembre-se de que `Long` tem uma largura de dados diferente (32 bits) em outros ambientes. Se você estiver passando um argumento de 32 bits para tal componente, declare-o como `Integer` em vez de `Long` no seu novo código do Visual Basic.  
  
-   **Ampliação.** O `Long` tipo de dados amplia a `Decimal`, `Single`, ou `Double`. Isso significa que você pode converter `Long` em qualquer um desses tipos sem a ocorrência de um erro <xref:System.OverflowException?displayProperty=nameWithType>.  
  
-   **Caracteres de tipo.** Acrescentar o caractere de tipo literal `L` a um literal o força ao tipo de dados `Long`. Acrescentar o caractere de tipo identificador `&` a qualquer identificador o força ao tipo `Long`.  
  
-   **Tipo de estrutura.** O tipo correspondente no .NET Framework é a estrutura <xref:System.Int64?displayProperty=nameWithType>.  

## <a name="see-also"></a>Consulte também

<xref:System.Int64>[Tipos de dados](../../../visual-basic/language-reference/data-types/data-type-summary.md)   
[Tipo de dados inteiro](../../../visual-basic/language-reference/data-types/integer-data-type.md)   
[Tipo de dados Short](../../../visual-basic/language-reference/data-types/short-data-type.md)   
[Funções de conversão de tipo](../../../visual-basic/language-reference/functions/type-conversion-functions.md)   
[Resumo da conversão](../../../visual-basic/language-reference/keywords/conversion-summary.md)   
[Uso Eficiente de Tipos de Dados](../../../visual-basic/programming-guide/language-features/data-types/efficient-use-of-data-types.md)
