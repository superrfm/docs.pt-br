---
title: "Abreviações de tipo (F#)"
description: "Saiba mais sobre F # abreviações de tipo para dar um nome mais significativo de um tipo para facilitar a leitura do código."
keywords: "visual f#, f#, programação funcional"
author: cartermp
ms.author: phcart
ms.date: 05/16/2016
ms.topic: language-reference
ms.prod: .net
ms.technology: devlang-fsharp
ms.devlang: fsharp
ms.assetid: 560af74f-935f-415c-af56-604cddb9da6b
ms.openlocfilehash: 235c0240fe89d203b9474dec2b3f91947f453cd8
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/18/2017
---
# <a name="type-abbreviations"></a>Abreviações de tipo

Um *abreviação de tipo* é um alias ou nome alternativo para um tipo.

## <a name="syntax"></a>Sintaxe

```fsharp
type type-abbreviation = type-name
```

## <a name="remarks"></a>Comentários
Você pode usar as abreviações de tipo para dar um nome mais significativo, de um tipo para facilitar a leitura do código. Você também pode usá-los para criar um nome fácil de usar um tipo que está inconveniente para gravar. Além disso, você pode usar abreviações de tipo para tornar mais fácil alterar um tipo subjacente sem alterar o código que usa o tipo. A seguir é uma abreviação de tipo simples.

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-1/snippet2301.fs)]

Abreviações de tipo podem incluir parâmetros genéricos, como no código a seguir.

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-1/snippet2302.fs)]

No código anterior, `Transform` é uma abreviação de tipo que representa uma função que aceita um único argumento de qualquer tipo e que retorna um único valor do mesmo tipo.

Abreviações de tipo não são preservadas no código MSIL do .NET Framework. Portanto, quando você usa um assembly F # de outra linguagem do .NET Framework, você deve usar o nome do tipo base para uma abreviação de tipo.

Abreviações de tipo também podem ser usadas em unidades de medida. Para obter mais informações, consulte [unidades de medida](units-of-measure.md).


## <a name="see-also"></a>Consulte também
[Referência da Linguagem F#](index.md)

