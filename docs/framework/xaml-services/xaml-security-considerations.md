---
title: "Considerações sobre segurança XAML"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-wpf
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- security [XAML Services], .NET XAML services
- XAML security [XAML Services]
ms.assetid: 544296d4-f38e-4498-af49-c9f4dad28964
caps.latest.revision: "7"
author: wadepickett
ms.author: wpickett
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: b58719f36cd911497c5cd892610330688221e7ef
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/22/2017
---
# <a name="xaml-security-considerations"></a>Considerações sobre segurança XAML
Este tópico descreve as práticas recomendadas de segurança em aplicativos quando você usar o XAML e API de serviços XAML do .NET Framework.  
  
## <a name="untrusted-xaml-in-applications"></a>XAML não confiável em aplicativos  
 No sentido mais geral, o XAML não confiável é qualquer fonte XAML que seu aplicativo não especificamente não incluem ou emitir.  
  
 XAML que é compilado em ou armazenado como um `resx`-tipo de recurso dentro de um assembly assinado e não confiáveis não é inerentemente confiável. Você pode confiar em XAML quanto você confia que o assembly como um todo. Na maioria dos casos, você só estiver preocupado com os aspectos de confiança XAML flexível, que é uma fonte XAML carregados a partir de um fluxo ou outras e/s. XAML livre não é um componente específico ou um recurso de um modelo de aplicativo com uma infra-estrutura de empacotamento e implantação. No entanto, um assembly pode implementar um comportamento que envolve o carregamento XAML flexível.  
  
 Para XAML não confiável, você deve tratá-lo geralmente o mesmo como se fosse o código não confiável. Usar modo seguro ou outros metáforas para evitar XAML possivelmente não confiável acessem seu código confiável.  
  
 A natureza de recursos XAML dá o direito de construir objetos e definir suas propriedades XAML. Esses recursos também incluem o acesso a conversores de tipo de mapeamento e acessando assemblies no domínio do aplicativo, usando as extensões de marcação, `x:Code` blocos e assim por diante.  
  
 Além de seus recursos de nível de linguagem XAML é usado para definição de interface do usuário em várias tecnologias. Carregamento XAML não confiável pode significar que carregar uma interface de usuário mal-intencionado falsificação.  
  
## <a name="sharing-context-between-readers-and-writers"></a>Compartilhamento de contexto entre leitores e gravadores  
 A arquitetura de serviços XAML do .NET Framework para leitores XAML e gravadores XAML geralmente requer o compartilhamento de um leitor de XAML para um gravador XAML ou um contexto de esquema XAML compartilhado. Compartilhamento de objetos ou contextos pode ser necessário se você estiver escrevendo uma lógica de loop do nó XAML ou fornecendo um personalizado salvar caminho. Você não deve compartilhar as instâncias de leitor XAML, contexto de esquema XAML não padrão ou configurações para classes de leitor/gravador XAML entre o código confiável e não confiáveis.  
  
 A maioria dos cenários e as operações que envolvem o objeto XAML escrevendo para um tipo de CLR fazendo poderá usar o contexto do esquema XAML padrão. O contexto do esquema XAML padrão não inclui configurações que possam comprometer a confiança total explicitamente. Portanto, é seguro compartilhar contexto entre componentes de leitor/gravador XAML confiáveis e não confiáveis. No entanto, se você fizer isso, ele ainda é uma prática recomendada para manter esses leitores e gravadores em separado <xref:System.AppDomain> escopos, com um deles especificamente pretendido/área restrita de confiança parcial.  
  
## <a name="xaml-namespaces-and-assembly-trust"></a>Namespaces XAML e a confiança do Assembly  
 A sintaxe básica de não-qualificado e definição como XAML interpreta um mapeamento de namespace XAML personalizado a um assembly não faz distinção entre um assembly confiável e como carregados para o domínio de aplicativo. Assim, é tecnicamente possível para um assembly não confiável falsificar o mapeamento de namespace XAML desejado de um assembly confiável e capturar um XAML declarado objeto de origem e informações de propriedade. Se você tiver requisitos de segurança para evitar essa situação, o mapeamento de namespace XAML desejado deve ser criado usando uma das seguintes técnicas:  
  
-   Use um nome totalmente qualificado do assembly com nome forte em qualquer mapeamento de namespace XAML feito pelo XAML do seu aplicativo.  
  
-   Restringir o assembly de mapeamento para um conjunto fixo de assemblies de referência, criando um determinado <xref:System.Xaml.XamlSchemaContext> para que o XAML leitores e XAML gravadores de objeto. Consulte <xref:System.Xaml.XamlSchemaContext.%23ctor%28System.Collections.Generic.IEnumerable%7BSystem.Reflection.Assembly%7D%29>.  
  
## <a name="xaml-type-mapping-and-type-system-access"></a>Mapeamento de tipo XAML e acesso de sistema de tipo  
 XAML dá suporte a seu próprio sistema de tipo, que é um par de como o CLR implementa o sistema básico de tipo CLR de várias maneiras. No entanto, para determinados aspectos de reconhecimento de tipo em que você decidir confiança sobre um tipo com base em suas informações de tipo, você deve adiar as informações de tipo CLR fazendo tipos. Isso ocorre porque alguns dos recursos de relatório específicos do sistema de tipo XAML são deixados abertos como métodos virtuais e, portanto, não são totalmente sob o controle das implementações de serviços XAML do .NET Framework do originais. Esses pontos de extensibilidade existem porque o sistema de tipo XAML é extensível, para corresponder a extensibilidade do próprio XAML e seus possíveis estratégias alternativas de mapeamento de tipo versus a implementação do padrão baseado em CLR e o contexto do esquema XAML padrão. Para obter mais informações, consulte as notas de específicas em várias das propriedades de <xref:System.Xaml.XamlType> e <xref:System.Xaml.XamlMember>.  
  
## <a name="see-also"></a>Consulte também  
 <xref:System.Xaml.Permissions.XamlAccessLevel>
