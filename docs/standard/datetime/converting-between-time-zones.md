---
title: "Convertendo horários entre fusos horários"
ms.custom: 
ms.date: 04/10/2017
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-standard
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- csharp
- vb
helpviewer_keywords:
- times [.NET Framework], converting
- time zones [.NET Framework], conversions
- UTC times, converting
- converting times
- local time conversions
ms.assetid: a51e1a3b-c983-4320-b31a-1f9fa3cf824a
caps.latest.revision: "19"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.workload:
- dotnet
- dotnetcore
ms.openlocfilehash: eabe0c1511e6fd42798f1a879e9e8d526d543a29
ms.sourcegitcommit: 91691981897cf8451033cb01071d8f5d94017f97
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/09/2018
---
# <a name="converting-times-between-time-zones"></a>Convertendo horários entre fusos horários

Está se tornando cada vez mais importante para qualquer aplicativo que trabalha com datas e horas lidar com diferenças entre fusos horários. Um aplicativo não pode assumir que todos os horários podem ser expressos na hora local, que é o tempo disponível do <xref:System.DateTime> estrutura. Por exemplo, uma página da Web que exibe a hora atual no leste dos Estados Unidos não terá credibilidade para um cliente no leste da Ásia. Este tópico explica como converter horas de um fuso horário para outro, bem como converter <xref:System.DateTimeOffset> valores que limitaram reconhecimento de fuso horário.

## <a name="converting-to-coordinated-universal-time"></a>Convertendo para o Tempo Universal Coordenado

O UTC (Tempo Universal Coordenado) é um padrão de tempo atômico de alta precisão. Os fusos horários do mundo são expressos como deslocamentos positivos ou negativos com relação ao UTC. Sendo assim, o UTC fornece uma espécie de hora livre de fuso horário ou com fuso horário neutro. O uso da hora em UTC é recomendado quando a portabilidade da data e hora entre computadores é importante. (Para obter detalhes e as melhores práticas usando datas e horas, consulte [práticas de codificação recomendadas usando DateTime no .NET Framework](https://msdn.microsoft.com/library/ms973825.aspx).) Converter fusos horários individuais em UTC facilita comparações de hora.

> [!NOTE]
> Você também pode serializar um <xref:System.DateTimeOffset> estrutura inequivocamente representam um único ponto no tempo. Porque <xref:System.DateTimeOffset> objetos armazenarem um valor de data e hora junto com seu deslocamento do UTC, eles sempre representam um ponto específico no tempo em relação ao UTC.

A maneira mais fácil para converter um horário para UTC é chamar o `static` (`Shared` no Visual Basic) <xref:System.TimeZoneInfo.ConvertTimeToUtc%28System.DateTime%29?displayProperty=nameWithType> método. A conversão exata executada pelo método depende do valor da `dateTime` do parâmetro <xref:System.DateTime.Kind%2A> propriedade, como mostra a tabela a seguir.

| `DateTime.Kind`            | Conversão                                                                     |
| -------------------------- | ------------------------------------------------------------------------------ |
| `DateTimeKind.Local`       | Converte a hora local para UTC.                                                    |
| `DateTimeKind.Unspecified` | Presume que o parâmetro `dateTime` é a hora local e converte a hora local para UTC. |
| `DateTimeKind.Utc`         | Retorna o parâmetro `dateTime` inalterado.                                    |

O código a seguir converte a hora local atual para UTC e exibe o resultado no console.

[!code-csharp[System.TimeZone2.Concepts#6](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.TimeZone2.Concepts/CS/TimeZone2Concepts.cs#6)]
[!code-vb[System.TimeZone2.Concepts#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.TimeZone2.Concepts/VB/TimeZone2Concepts.vb#6)]

> [!NOTE]
> O <xref:System.TimeZoneInfo.ConvertTimeToUtc%28System.DateTime%29?displayProperty=nameWithType> método necessariamente não produzir resultados idênticos a <xref:System.TimeZone.ToUniversalTime%2A?displayProperty=nameWithType> e <xref:System.DateTime.ToUniversalTime%2A?displayProperty=nameWithType> métodos. Se o sistema do host local do fuso horário inclui várias regras de ajuste, <xref:System.TimeZoneInfo.ConvertTimeToUtc%28System.DateTime%29?displayProperty=nameWithType> se aplica a regra apropriada para uma determinada data e hora. Os outros dois métodos sempre aplicam a regra de ajuste mais recente.

Se o valor de data e hora não representarem o horário local ou UTC, o <xref:System.DateTime.ToUniversalTime%2A> método provavelmente retornará um resultado errado. No entanto, você pode usar o <xref:System.TimeZoneInfo.ConvertTimeToUtc%2A?displayProperty=nameWithType> método para converter a data e hora de uma zona de tempo especificada. (Para obter detalhes sobre como recuperar um <xref:System.TimeZoneInfo> objeto que representa o fuso horário de destino, consulte [encontrando os fusos horários definidos em um sistema local](../../../docs/standard/datetime/finding-the-time-zones-on-local-system.md).) O código a seguir usa o <xref:System.TimeZoneInfo.ConvertTimeToUtc%2A?displayProperty=nameWithType> método para converter o horário padrão Oriental para UTC.

[!code-csharp[System.TimeZone2.Concepts#7](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.TimeZone2.Concepts/CS/TimeZone2Concepts.cs#7)]
[!code-vb[System.TimeZone2.Concepts#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.TimeZone2.Concepts/VB/TimeZone2Concepts.vb#7)]

Observe que este método lança um <xref:System.ArgumentException> se o <xref:System.DateTime> do objeto <xref:System.DateTime.Kind%2A> propriedade e o fuso horário são incompatíveis. Uma incompatibilidade ocorre se o <xref:System.DateTime.Kind%2A> é de propriedade <xref:System.DateTimeKind?displayProperty=nameWithType> , mas o <xref:System.TimeZoneInfo> objeto não representam o fuso horário local, ou se o <xref:System.DateTime.Kind%2A> é de propriedade <xref:System.DateTimeKind?displayProperty=nameWithType> , mas o <xref:System.TimeZoneInfo> não é igual ao objeto <xref:System.DateTimeKind?displayProperty=nameWithType>.

Todos esses métodos levam <xref:System.DateTime> valores como parâmetros e retornam um <xref:System.DateTime> valor. Para <xref:System.DateTimeOffset> valores, o <xref:System.DateTimeOffset> estrutura tem um <xref:System.DateTimeOffset.ToUniversalTime%2A> método que converte a data e hora da instância atual em UTC de instância. A exemplo a seguir chama o <xref:System.DateTimeOffset.ToUniversalTime%2A> método para converter a hora local e várias outras horas em tempo Universal Coordenado (UTC).

[!code-csharp[System.DateTimeOffset.Methods#16](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Methods/cs/Methods.cs#16)]
[!code-vb[System.DateTimeOffset.Methods#16](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Methods/vb/Methods.vb#16)]

## <a name="converting-utc-to-a-designated-time-zone"></a>Convertendo UTC em um fuso horário designado

Para converter UTC para o horário local, consulte a seção "converter UTC para Hora Local" que segue. Para converter UTC para o horário em qualquer fuso horário que você designar, chame o <xref:System.TimeZoneInfo.ConvertTimeFromUtc%2A> método. O método utiliza dois parâmetros:

* O UTC a ser convertido. Isso deve ser um <xref:System.DateTime> valor cuja <xref:System.DateTime.Kind%2A> está definida como `Unspecified` ou `Utc`.

* O fuso horário no qual o UTC deve ser convertido.

O código a seguir converte o UTC para o Horário Padrão Central.

[!code-csharp[System.TimeZone2.Concepts#8](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.TimeZone2.Concepts/CS/TimeZone2Concepts.cs#8)]
[!code-vb[System.TimeZone2.Concepts#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.TimeZone2.Concepts/VB/TimeZone2Concepts.vb#8)]

## <a name="converting-utc-to-local-time"></a>Convertendo UTC em hora local

Para converter UTC para a hora local, chame o <xref:System.DateTime.ToLocalTime%2A> método o <xref:System.DateTime> objeto cujo tempo você deseja converter. O comportamento exato do método depende do valor do objeto <xref:System.DateTime.Kind%2A> propriedade, como mostra a tabela a seguir.

| `DateTime.Kind`            | Conversão                                                                               |
| -------------------------- | ---------------------------------------------------------------------------------------- |
| `DateTimeKind.Local`       | Retorna o <xref:System.DateTime> valor inalterado.                                      |
| `DateTimeKind.Unspecified` | Assume que o <xref:System.DateTime> valor é UTC e converte UTC para a hora local. |
| `DateTimeKind.Utc`         | Converte o <xref:System.DateTime> valor para a hora local.                                 |

> [!NOTE]
> O <xref:System.TimeZone.ToLocalTime%2A?displayProperty=nameWithType> método se comporta de forma idêntica ao `DateTime.ToLocalTime` método. Ele usa um único parâmetro, que é o valor de data e hora para converter.

Você também pode converter a hora em qualquer fuso horário designado para o horário local usando o `static` (`Shared` no Visual Basic) <xref:System.TimeZoneInfo.ConvertTime%2A?displayProperty=nameWithType> método. Essa técnica é abordada na próxima seção.

## <a name="converting-between-any-two-time-zones"></a>Convertendo entre dois fusos horários

Você pode converter entre quaisquer dois fusos horários usando qualquer um dos dois seguintes `static` (`Shared` no Visual Basic) métodos de <xref:System.TimeZoneInfo> classe:

* <xref:System.TimeZoneInfo.ConvertTime%2A>

  Esses parâmetros do método são o valor de data e hora a ser convertido, um `TimeZoneInfo` objeto que representa o fuso horário do valor de data e hora, e um `TimeZoneInfo` objeto que representa o fuso horário para converter o valor de data e hora para.

* <xref:System.TimeZoneInfo.ConvertTimeBySystemTimeZoneId%2A>

  Esses parâmetros do método são a data e valor de tempo para converter, o identificador de data e fuso horário do valor de hora e o identificador do fuso horário para converter o valor de data e hora para.

Ambos os métodos requerem que o <xref:System.DateTime.Kind%2A> propriedade do valor de data e hora para converter e <xref:System.TimeZoneInfo> o identificador de objeto ou o fuso horário que representa seu fuso horário corresponder um ao outro. Caso contrário, um <xref:System.ArgumentException> será gerado. Por exemplo, se o `Kind` é de propriedade do valor de data e hora `DateTimeKind.Local`, uma exceção será lançada se o `TimeZoneInfo` objeto passado como um parâmetro para o método não é igual a `TimeZoneInfo.Local`. Também é apresentada uma exceção se o identificador passado como um parâmetro para o método não é igual a `TimeZoneInfo.Local.Id`.

O exemplo a seguir usa o <xref:System.TimeZoneInfo.ConvertTime%2A> método para converter hora oficial do Havaí para a hora local.

[!code-csharp[System.TimeZone2.Concepts#9](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.TimeZone2.Concepts/CS/TimeZone2Concepts.cs#9)]
[!code-vb[System.TimeZone2.Concepts#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.TimeZone2.Concepts/VB/TimeZone2Concepts.vb#9)]

## <a name="converting-datetimeoffset-values"></a>Convertendo valores de DateTimeOffset

Valores de data e hora representados pelo <xref:System.DateTimeOffset> objetos não são totalmente fuso horário com suporte porque o objeto é desassociado do seu fuso horário no momento em que ele é instanciado. No entanto, em muitos casos o aplicativo precisa apenas converter uma data e hora com base em dois deslocamentos diferentes do UTC, em vez da hora em fusos horários específicos. Para realizar essa conversão, você pode chamar a instância atual <xref:System.DateTimeOffset.ToOffset%2A> método. O parâmetro do método único é o deslocamento do novo valor de data e hora que o método deve retornar.

Por exemplo, se a data e hora da solicitação de um usuário de uma página da Web for conhecida e for serializada como uma cadeia de caracteres no formato MM/dd/aaaa hh:mm:ss zzzz, o seguinte método `ReturnTimeOnServer` converte esse valor de data e hora para a data e hora no servidor Web.

[!code-csharp[System.DateTimeOffset.Conceptual.OffsetConversions#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.OffsetConversions/cs/TimeConversions.cs#1)]
[!code-vb[System.DateTimeOffset.Conceptual.OffsetConversions#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.OffsetConversions/vb/TimeConversions.vb#1)] 

Se a cadeia de caracteres "9/1/2007 5:32:07 -05:00" for passada ao método, representando a data e hora em um fuso horário cinco horas anteriores ao UTC, ele retornará 9/1/2007 3:32:07 AM -07:00 para um servidor localizado nos EUA. Fuso horário padrão do Pacífico.

O <xref:System.TimeZoneInfo> classe também inclui uma sobrecarga de <xref:System.TimeZoneInfo.ConvertTime%28System.DateTimeOffset%2CSystem.TimeZoneInfo%29?displayProperty=nameWithType> método que executa conversões de fuso horário com <xref:System.DateTimeOffset.ToOffset(System.TimeSpan)> valores. Os parâmetros do método são um <xref:System.DateTimeOffset> valor e uma referência para o fuso horário para o qual a hora será convertido. A chamada do método retorna um <xref:System.DateTimeOffset> valor. Por exemplo, o `ReturnTimeOnServer` método no exemplo anterior poderia ser reescrito da seguinte maneira para chamar o <xref:System.TimeZoneInfo.ConvertTime%28System.DateTimeOffset%2CSystem.TimeZoneInfo%29> método.

[!code-csharp[System.DateTimeOffset.Conceptual.OffsetConversions#2](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.OffsetConversions/cs/timeconversions2.cs#2)]
[!code-vb[System.DateTimeOffset.Conceptual.OffsetConversions#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.OffsetConversions/vb/TimeConversions2.vb#2)]

## <a name="see-also"></a>Consulte também

<xref:System.TimeZoneInfo>[Datas, horas e fusos horários](../../../docs/standard/datetime/index.md)
[encontrando os fusos horários definidos em um sistema local](../../../docs/standard/datetime/finding-the-time-zones-on-local-system.md)
