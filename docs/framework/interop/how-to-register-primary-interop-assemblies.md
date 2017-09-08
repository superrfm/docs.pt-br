---
title: "Como registrar assemblies de interoperabilidade primários"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- registering primary interop assemblies
- primary interop assemblies, registering
ms.assetid: 4b2fcf8a-429d-43ce-8334-e026040be8bb
caps.latest.revision: 8
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 81b57a73b8c5118af9cf2867902b849d73820e83
ms.contentlocale: pt-br
ms.lasthandoff: 08/21/2017

---
# <a name="how-to-register-primary-interop-assemblies"></a>Como registrar assemblies de interoperabilidade primários
As classes podem ter o marshaling realizado somente pela interoperabilidade COM e sempre têm o marshaling realizado como interfaces. Em alguns casos, a interface usada para realizar marshaling da classe é conhecida como a interface de classe. Para obter informações sobre como substituir a interface de classe por uma interface de sua preferência, consulte [COM Callable Wrapper](../../../docs/framework/interop/com-callable-wrapper.md).  
  
 Embora qualquer desenvolvedor que deseje usar tipos COM de um aplicativo do .NET Framework possa gerar um assembly de interoperabilidade, fazer isso cria um problema. Cada vez que um desenvolvedor importa e assina uma biblioteca de tipos COM, o desenvolvedor cria um conjunto de tipos exclusivos que são incompatíveis com aqueles importados e assinados por outro desenvolvedor. A solução para esse problema de incompatibilidade de tipo é que cada desenvolvedor obtenha o assembly de interoperabilidade primário assinado e fornecido pelo fornecedor.  
  
 Se você pretende expor os tipos COM terceiros para outros aplicativos, use sempre o assembly de interoperabilidade primário fornecido pelo mesmo editor da biblioteca de tipos que esse assembly define. Além de fornecer compatibilidade garantida, os assemblies de interoperabilidade primários geralmente são personalizados pelo fornecedor para aprimorar a interoperabilidade.  
  
 Mesmo se você não planeja expor os tipos COM terceiros, usar o assembly de interoperabilidade primário pode facilitar a tarefa de interoperar com componentes COM. No entanto, essa estratégia não fornece nenhum isolamento de alterações que um fornecedor possa fazer a tipos definidos em um assembly de interoperabilidade primário. Quando seu aplicativo requer um isolamento desse tipo, gere seu próprio assembly de interoperabilidade em vez de usar o assembly de interoperabilidade primário.  
  
 Você deve registrar todos os assemblies de interoperabilidade primários adquiridos no computador de desenvolvimento antes que você possa referenciá-los com [!INCLUDE[vsprvsext](../../../includes/vsprvsext-md.md)]. O Visual Studio procura e usa um assembly de interoperabilidade primário na primeira vez que você referenciar um tipo de uma biblioteca de tipos COM. Se o Visual Studio não puder localizar o assembly de interoperabilidade primário associado à biblioteca de tipos, ele solicitará que você o adquira ou oferecerá a possibilidade de criar um assembly de interoperabilidade em vez disso. Da mesma forma, o [Importador de Biblioteca de Tipos (Tlbimp.exe)](../../../docs/framework/tools/tlbimp-exe-type-library-importer.md) também usa o Registro para localizar assemblies de interoperabilidade primários.  
  
 Embora não seja necessário registrar assemblies de interoperabilidade primários a menos que você planeje usar o Visual Studio, o registro fornece duas vantagens:  
  
-   Um assembly de interoperabilidade primário registrado é claramente marcado na chave do Registro da biblioteca de tipos original. O registro é a melhor maneira de localizar um assembly de interoperabilidade primário em seu computador.  
  
-   Você pode evitar gerar acidentalmente e usar um novo assembly de interoperabilidade se, em algum momento no futuro, você usar o Visual Studio para fazer referência a um tipo para o qual você tem um assembly de interoperabilidade primário não registrado.  
  
 Use a [Ferramenta de Registro do Assembly (Regasm.exe)](../../../docs/framework/tools/regasm-exe-assembly-registration-tool.md) para registrar um assembly de interoperabilidade primário.  
  
### <a name="to-register-a-primary-interop-assembly"></a>Para registrar um assembly de interoperabilidade primário  
  
1.  No prompt de comando, digite:  
  
     **regasm** *nomedoassembly*  
  
     Nesse comando, *nomedoassembly* é o nome do arquivo do assembly que é registrado. Regasm.exe adiciona uma entrada para o assembly de interoperabilidade primário sob a mesma chave do Registro da biblioteca de tipos original.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir registra o assembly de interoperabilidade primário `CompanyA.UtilLib.dll`.  
  
```  
regasm CompanyA.UtilLib.dll  
```  
  
## <a name="see-also"></a>Consulte também  
 [Programando com assemblies de interoperabilidade primários](http://msdn.microsoft.com/en-us/306fa1d6-0703-4004-9e93-d0a57f1be81e)   
 [Localizando assemblies de interoperabilidade primários](http://msdn.microsoft.com/en-us/d6768e4b-cd80-414d-a4f8-05d979eb393b)   
 [Redistribuindo assemblies de interoperabilidade primários](http://msdn.microsoft.com/en-us/e76384f0-d631-474c-bdbd-13884cba0265)
