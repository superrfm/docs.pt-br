---
title: "Uso de instância padrão de uma classe no construtor da classe pode levar a chamada recursiva infinita"
ms.date: 07/20/2015
ms.prod: .net
ms.technology: devlang-visual-basic
ms.topic: article
ms.assetid: 9645b47f-7de5-46d0-bb45-d5fdaa8aaa2a
caps.latest.revision: "13"
author: dotnet-bot
ms.author: dotnetcontent
ms.openlocfilehash: 6a0c54c6e62f9bdc7fe510500a486461d26636d8
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/18/2017
---
# <a name="use-of-default-instance-of-a-class-in-the-class-constructor-could-lead-to-infinite-recursive-call"></a>Uso de instância padrão de uma classe no construtor da classe pode levar a chamada recursiva infinita
Uma instância padrão de uma classe foi usada no construtor da classe. Isso pode levar a uma chamada recursiva infinita, também conhecido como um loop infinito.  
  
## <a name="to-correct-this-error"></a>Para corrigir este erro  
  
-   Remova a instância padrão do construtor da classe.  
  
## <a name="see-also"></a>Consulte também  
 [Construtores](~/docs/visual-basic/programming-guide/concepts/object-oriented-programming.md#constructors)
