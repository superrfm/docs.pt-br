---
title: "Quando implantar contêineres do Windows para serviço de contêiner do Azure (ou seja, Kubernetes)"
description: "Arquitetura de Microservices .NET para aplicativos .NET em contêineres | Quando implantar contêineres do Windows para serviço de contêiner do Azure (ou seja, Kubernetes)"
author: CESARDELATORRE
ms.author: wiwagn
ms.date: 10/26/2017
ms.workload:
- dotnet
- dotnetcore
ms.openlocfilehash: 2f7ed0c9ebf1c80ae6cae4311b2682d3cc161623
ms.sourcegitcommit: e7f04439d78909229506b56935a1105a4149ff3d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/23/2017
---
# <a name="when-to-deploy-windows-containers-to-azure-container-service-that-is-kubernetes"></a>Quando implantar contêineres do Windows para serviço de contêiner do Azure (ou seja, Kubernetes)

Serviço de contêiner do Azure otimiza a configuração de tecnologias e ferramentas de código aberto populares especificamente para o Azure. Você obtém uma solução aberta que oferece portabilidade para seus contêineres e sua configuração de aplicativo. Você seleciona o tamanho, o número de hosts e as ferramentas do orchestrator. Serviço de contêiner do Azure lida com a infraestrutura para você.

Se você já estiver trabalhando com código-fonte aberto orchestrators como Kubernetes, Docker Swarm ou DC/sistema operacional, você não precisa alterar suas práticas de gerenciamento existente para mover cargas de trabalho do contêiner para a nuvem. Use as ferramentas de gerenciamento de aplicativo que você já estiver familiarizado com e conectar-se por meio de pontos de extremidade de API padrão para o orquestrador de sua escolha.

Todos esses orchestrators são ambientes maduras se você estiver usando contêineres do Docker do Linux, mas eles também suporte contêineres do Windows de 2017 (alguns anteriormente, outros mais recentemente, dependendo do orchestrator).

Por exemplo, em Kubernetes, o suporte para contêineres é nativo (cidadão de primeira classe), portanto, usar contêineres do Windows em Kubernetes também é muito eficiente e confiável (em visualização até logo se enquadram 2017).

>[!div class="step-by-step"]
[Anterior](when-to-deploy-windows-containers-to-service-fabric.md)
[Próximo](build-resilient-services-ready-for-the-cloud-embrace-transient-failures-in-the-cloud.md)
