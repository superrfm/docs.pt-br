---
title: Malhas ponto a ponto
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d93e312e-ac04-40f8-baea-5da1cacb546e
caps.latest.revision: "9"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 0f70c1dfba6ceb53cd674726702c471dbe508d46
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/22/2017
---
# <a name="peer-meshes"></a>Malhas ponto a ponto
Um *malha* é um conjunto nomeado (um gráfico interconectado) de nós ponto que pode se comunicar entre si e que são identificados por uma ID exclusiva de malha Cada nó é conectado a vários outros nós. Em uma malha bem conectada, há um caminho entre dois nós, com poucas saltos entre os nós as bordas mais distante da malha, e a malha permanecerão conectada, mesmo que alguns nós ou conexões diminuir. Nós ativos de malha publicam suas informações de ponto de extremidade com uma ID de malha correspondente para que outros pares podem encontrá-los.  
  
## <a name="characteristics-of-a-mesh-created-using-peer-channel"></a>Características de uma malha criado usando o canal par  
  
#### <a name="uniquely-identified"></a>Identificada exclusivamente  
  
-   Uma ID exclusiva identifica cada malha. O nome da malha (ou ID de malha) é o mesmo formato, como um nome de host do sistema de nome de domínio (DNS). Como tal, essa ID de malha deve ser exclusivo para o cliente pretendido do aplicativo dentro do escopo do resolvedor que está sendo usado. Um nome comum, como "MyFamilysPeers" ou "KevinsPokerTable" facilmente entrem em conflito com outros nomes de usuário e pode retornar informações de ponto de extremidade, o que podem resultar em problemas de privacidade ou aumentar a latência de conexão de ponto a ponto não intencional. Pode ser uma maneira para evitar esses problemas adicionar uma ID exclusiva como um sufixo para o apelido para a malha (por exemplo, "KevinsPokerTable90210").  
  
#### <a name="message-flooding"></a>Saturação de mensagem  
  
-   A malha permite que mensagens sejam propagadas de um ou mais remetentes para todos os outros nós de mesmo nível na mesma malha. Mensagens distribuídas por nós do par usam cabeçalhos especificados no namespace em `http://schemas.microsoft.com/net/2006/05/peer`.  
  
#### <a name="optimized-connections"></a>Conexões otimizados  
  
-   Uma malha de canal par ajusta automaticamente quando nós ingressar e sair, garantindo que todos os nós têm boa conectividade com pouca chance de criação de partições (grupos de nós isoladas umas das outras). Conexões na malha são otimizadas também dinamicamente com base nos padrões de tráfego atual, para que a latência de mensagem do remetente ao destinatário é o menor possível.  
  
#### <a name="popular-network-features-that-peer-channel-does-not-provide"></a>Recursos de rede populares que não fornece um canal par  
 É importante estar ciente dos recursos de rede comum que não fornece um canal par. Esses recursos, que todos podem ser criados na parte superior de canal par, incluem o seguinte:  
  
-   **Classificação de mensagem:** mensagens provenientes de uma única fonte não podem chegar em todos os outros participantes na mesma ordem ou na ordem em que é enviada a origem. Aplicativos que necessitam de mensagens ser entregue em uma determinada ordem deve compilá-lo em seus aplicativos (por exemplo, ao incluir uma ID monotônica com todas as mensagens).  
  
-   **Mensagens confiáveis:** canal par não inclui um mecanismo para garantir a recepção de mensagem por todos os pares. Para garantir a entrega de mensagens, você deve escrever uma camada de confiabilidade sobre canal par.
