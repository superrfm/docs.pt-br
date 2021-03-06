---
title: Carregando dados em um DataSet
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-ado
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- csharp
- vb
ms.assetid: a53e5dc1-9669-49d4-828d-efa633237066
caps.latest.revision: "2"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: dotnet
ms.openlocfilehash: 4be4c1aa449c3bd78774c6aafe1ec2b55b27b663
ms.sourcegitcommit: ed26cfef4e18f6d93ab822d8c29f902cff3519d1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/17/2018
---
# <a name="loading-data-into-a-dataset"></a>Carregando dados em um DataSet
Um objeto <xref:System.Data.DataSet> deve ser populado primeiro para que você possa consultá-lo com o [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)]. Há várias maneiras diferentes de popular o <xref:System.Data.DataSet>. Por exemplo, você pode usar [!INCLUDE[vbtecdlinq](../../../../includes/vbtecdlinq-md.md)] para consultar o banco de dados e carregar os resultados para o <xref:System.Data.DataSet>. Para obter mais informações, consulte [LINQ to SQL](../../../../docs/framework/data/adonet/sql/linq/index.md).  
  
 Outra maneira comum de carregar dados em um <xref:System.Data.DataSet> é usar a classe <xref:System.Data.Common.DataAdapter> para recuperar dados do banco de dados. Isso é ilustrado no exemplo a seguir.  
  
## <a name="example"></a>Exemplo  
 Esse exemplo usa <xref:System.Data.Common.DataAdapter> para consultar o banco de dados AdventureWorks para obter informações sobre as vendas do ano 2002 e carrega os resultados em um <xref:System.Data.DataSet>. Depois que o <xref:System.Data.DataSet> foi populado, você pode escrever consultas nele usando o [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)]. O `FillDataSet` método neste exemplo é usado em consultas de exemplo [LINQ to DataSet exemplos](../../../../docs/framework/data/adonet/linq-to-dataset-examples.md). Para obter mais informações, consulte [consultar conjuntos de dados](../../../../docs/framework/data/adonet/querying-datasets-linq-to-dataset.md).  
  
 [!code-csharp[DP LINQ to DataSet Examples#FillDataSet](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#filldataset)]
 [!code-vb[DP LINQ to DataSet Examples#FillDataSet](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#filldataset)]  
  
## <a name="see-also"></a>Consulte também  
 [Visão geral de LINQ to DataSet](../../../../docs/framework/data/adonet/linq-to-dataset-overview.md)  
 [Consultando DataSets](../../../../docs/framework/data/adonet/querying-datasets-linq-to-dataset.md)  
 [Exemplos de LINQ to DataSet](../../../../docs/framework/data/adonet/linq-to-dataset-examples.md)
