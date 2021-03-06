---
title: "Opções de criação de atividade de WF"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b9061f5f-12c3-47f0-adbe-1330e2714c94
caps.latest.revision: "20"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 0422b7b433c8c2a6889e00d559207d25ed42eff1
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/22/2017
---
# <a name="activity-authoring-options-in-wf"></a>Opções de criação de atividade de WF
[!INCLUDE[netfx_current_long](../../../includes/netfx-current-long-md.md)] fornece várias opções para criar atividades personalizados. O método correto para usar para criar uma atividade determinada depende de quais recursos de tempo de execução são necessários.  
  
## <a name="deciding-which-base-activity-class-to-use-for-authoring-custom-activities"></a>Decidindo qual classe base de atividade usar para criar atividades personalizados  
 A tabela a seguir lista recursos disponíveis nas classes base personalizados de atividade.  
  
|Classe base de atividade|Recursos disponível|  
|-------------------------|------------------------|  
|<xref:System.Activities.Activity>|Composta grupos de sistema fornecido e atividades personalizadas em uma atividade composta.|  
|<xref:System.Activities.CodeActivity>|Implementa a funcionalidade imperativa fornecendo um método de <xref:System.Activities.CodeActivity%601.Execute%2A> que pode ser substituído. Também fornece acesso a acompanhar, a variáveis, e a argumentos.|  
|<xref:System.Activities.NativeActivity>|Fornece todos os recursos de <xref:System.Activities.CodeActivity>, mais nulo a execução da atividade, cancelar a execução filho da atividade, o uso de indexadores, e agendar atividades, ações de atividade, e funções.|  
|<xref:System.Activities.DynamicActivity>|Fornece uma abordagem de DOM semelhante à construção de atividades que interage com o designer do WF e o mecanismo de tempo de execução por meio de <!--zz <xref:System.ComponentModel.IcustomTypeDescriptor>--> `IcustomTypeDescriptor`, permitindo que as novas atividades a ser criado sem definir novos tipos.|  
  
## <a name="authoring-activities-using-activity"></a>Atividades de design usando a atividade  
 As atividades que derivam de <xref:System.Activities.Activity> compor a funcionalidade montando outras atividades existentes. Essas atividades podem ser atividades personalizados existentes e atividades de biblioteca de atividade de [!INCLUDE[netfx_current_long](../../../includes/netfx-current-long-md.md)] . Montar as atividades é a maneira mais básica de criar a funcionalidade personalizada. Essa abordagem é mais normalmente efetuado ao usar um ambiente de design visual para criar fluxos de trabalho.  
  
## <a name="authoring-activities-using-codeactivity-or-asynccodeactivity"></a>Atividades de design usando CodeActivity ou AsyncCodeActivity  
 As atividades que derivam de <xref:System.Activities.CodeActivity> ou de <xref:System.Activities.AsyncCodeActivity> podem implementar a funcionalidade imperativa substituindo o método de <xref:System.Activities.CodeActivity%601.Execute%2A> com código obrigatório personalizado. O código personalizado é executado quando a atividade é executada em tempo de execução. Quando as atividades criadas dessa maneira tenham acesso à funcionalidade personalizada, não tem acesso a todos os recursos de tempo de execução, como acesso completo para o ambiente de execução, a capacidade agendar atividades filhos, a criação do indexador, ou o suporte para um método de cancelamento ou de abort. Quando <xref:System.Activities.CodeActivity> executa, tem acesso a uma versão reduzida do ambiente de execução (por meio da classe <xref:System.Activities.CodeActivityContext> ou de <xref:System.Activities.AsyncCodeActivityContext> ). As atividades criadas usando <xref:System.Activities.CodeActivity> têm acesso a resolução do argumento e da variável, às extensões, e rastrear. Programação assíncrona de atividade pode ser feita usando <xref:System.Activities.AsyncCodeActivity>.  
  
## <a name="authoring-activities-using-nativeactivity"></a>Atividades de design usando NativeActivity  
 As atividades que derivam de <xref:System.Activities.NativeActivity>, como aqueles que derivam de <xref:System.Activities.CodeActivity>, criam a funcionalidade imperativa substituindo <xref:System.Activities.NativeActivity.Execute%2A>, mas também têm acesso a qualquer funcionalidade de tempo de execução de fluxo de trabalho com <xref:System.Activities.NativeActivityContext> que é passado para o método de <xref:System.Activities.NativeActivity.Execute%2A> . Neste contexto tem suporte para agendamento e Cancelando atividades filho, executando <xref:System.Activities.ActivityAction> e <!--zz <xref:System.Activities.ActivityFunc>--> `ActivityFunc` objetos de fluxo de transações em um fluxo de trabalho, invocando assíncronos processos, cancelando e anulando execução, acessem Propriedades de execução e as extensões e indicadores (identificadores de retomada de fluxos de trabalho em pausa).  
  
## <a name="authoring-activities-using-dynamicactivity"></a>Atividades de design usando DynamicActivity  
 Diferentemente de outros três tipos de atividade, a nova funcionalidade não é criada criando novos tipos de <xref:System.Activities.DynamicActivity> (a classe é fechada), mas em vez disso, montando funcionalidade em <xref:System.Activities.DynamicActivity.Properties%2A> e as propriedades de <xref:System.Activities.DynamicActivity.Implementation%2A> que usam uma atividade documentam o modelo de objeto (DOM).  
  
## <a name="authoring-activities-that-return-a-result"></a>Atividades de design que retornam um resultado  
 Muitas atividades deve retornar um resultado após sua execução. Embora seja possível definir sempre essa finalidade <xref:System.Activities.OutArgument%601> personalizado em uma atividade, é para usar <xref:System.Activities.Activity%601>, ou derivar de <xref:System.Activities.CodeActivity%601> ou de <xref:System.Activities.NativeActivity%601>. Cada uma dessas classes base tem <xref:System.Activities.OutArgument%601> nomeado o resultado da atividade pode usar para o seu valor de retorno. As atividades que retornam um resultado devem ser utilizadas somente se apenas um resultado precisa ser retornado de uma atividade; se vários resultados precisam ser retornados, os membros separados de <xref:System.Activities.OutArgument%601> devem ser usados em vez disso.
