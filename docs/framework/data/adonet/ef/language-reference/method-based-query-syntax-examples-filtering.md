---
title: "Exemplos de sintaxe da consulta baseada em método: filtragem"
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
ms.assetid: e40e314c-eb30-4f44-a054-41e511e35832
caps.latest.revision: "3"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: b81e163a6d326135f8031c6ef43af698d9c706b3
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/18/2017
---
# <a name="method-based-query-syntax-examples-filtering"></a><span data-ttu-id="d626e-102">Exemplos de sintaxe da consulta baseada em método: filtragem</span><span class="sxs-lookup"><span data-stu-id="d626e-102">Method-Based Query Syntax Examples: Filtering</span></span>
<span data-ttu-id="d626e-103">Os exemplos neste tópico demonstram como usar o `Where` e `Where…Contains` métodos para consultar o [modelo de vendas do AdventureWorks](http://msdn.microsoft.com/en-us/f16cd988-673f-4376-b034-129ca93c7832) usando a sintaxe de consulta com base em método.</span><span class="sxs-lookup"><span data-stu-id="d626e-103">The examples in this topic demonstrate how to use the `Where` and `Where…Contains` methods to query the [AdventureWorks Sales Model](http://msdn.microsoft.com/en-us/f16cd988-673f-4376-b034-129ca93c7832) using method-based query syntax.</span></span> <span data-ttu-id="d626e-104">Observe que, onde...`Contains`</span><span class="sxs-lookup"><span data-stu-id="d626e-104">Note, Where…`Contains`</span></span> <span data-ttu-id="d626e-105">não pode ser usado como parte de um [compilado consulta](../../../../../../docs/framework/data/adonet/ef/language-reference/compiled-queries-linq-to-entities.md).</span><span class="sxs-lookup"><span data-stu-id="d626e-105">cannot be used as a part of a [compiled query](../../../../../../docs/framework/data/adonet/ef/language-reference/compiled-queries-linq-to-entities.md).</span></span>  
  
 <span data-ttu-id="d626e-106">O Modelo de vendas AdventureWorks usado nesses exemplos é criado a partir das tabelas Contact, Address, Product, SalesOrderHeader e SalesOrderDetail no banco de dados de exemplo AdventureWorks.</span><span class="sxs-lookup"><span data-stu-id="d626e-106">The AdventureWorks Sales model used in these examples is built from the Contact, Address, Product, SalesOrderHeader, and SalesOrderDetail tables in the AdventureWorks sample database.</span></span>  
  
 <span data-ttu-id="d626e-107">Os exemplos neste tópico usam o seguinte `using` / `Imports` instruções:</span><span class="sxs-lookup"><span data-stu-id="d626e-107">The examples in this topic use the following `using`/`Imports` statements:</span></span>  
  
 [!code-csharp[DP L2E Examples#ImportsUsing](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Examples/CS/Program.cs#importsusing)]
 [!code-vb[DP L2E Examples#ImportsUsing](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Examples/VB/Module1.vb#importsusing)]  
  
## <a name="where"></a><span data-ttu-id="d626e-108">Where</span><span class="sxs-lookup"><span data-stu-id="d626e-108">Where</span></span>  
  
### <a name="example"></a><span data-ttu-id="d626e-109">Exemplo</span><span class="sxs-lookup"><span data-stu-id="d626e-109">Example</span></span>  
 <span data-ttu-id="d626e-110">O exemplo a seguir retorna todos os pedidos online.</span><span class="sxs-lookup"><span data-stu-id="d626e-110">The following example returns all online orders.</span></span>  
  
 [!code-csharp[DP L2E Examples#Where1_MQ](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Examples/CS/Program.cs#where1_mq)]
 [!code-vb[DP L2E Examples#Where1_MQ](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Examples/VB/Module1.vb#where1_mq)]  
  
### <a name="example"></a><span data-ttu-id="d626e-111">Exemplo</span><span class="sxs-lookup"><span data-stu-id="d626e-111">Example</span></span>  
 <span data-ttu-id="d626e-112">O exemplo a seguir retorna os pedidos onde a quantidade é maior que 2 e menor que 6.</span><span class="sxs-lookup"><span data-stu-id="d626e-112">The following example returns the orders where the order quantity is greater than 2 and less than 6.</span></span>  
  
 [!code-csharp[DP L2E Examples#Where2_MQ](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Examples/CS/Program.cs#where2_mq)]
 [!code-vb[DP L2E Examples#Where2_MQ](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Examples/VB/Module1.vb#where2_mq)]  
  
### <a name="example"></a><span data-ttu-id="d626e-113">Exemplo</span><span class="sxs-lookup"><span data-stu-id="d626e-113">Example</span></span>  
 <span data-ttu-id="d626e-114">O exemplo a seguir retorna todos os produtos vermelhos.</span><span class="sxs-lookup"><span data-stu-id="d626e-114">The following example returns all red colored products.</span></span>  
  
 [!code-csharp[DP L2E Examples#Where3_MQ](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Examples/CS/Program.cs#where3_mq)]
 [!code-vb[DP L2E Examples#Where3_MQ](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Examples/VB/Module1.vb#where3_mq)]  
  
### <a name="example"></a><span data-ttu-id="d626e-115">Exemplo</span><span class="sxs-lookup"><span data-stu-id="d626e-115">Example</span></span>  
 <span data-ttu-id="d626e-116">O exemplo a seguir usa o método `Where` para localizar os pedidos que foram feitos depois de 1° de dezembro de 2003 e, em seguida, usa a propriedade de navegação `order.SalesOrderDetail` para obter os detalhes de cada pedido.</span><span class="sxs-lookup"><span data-stu-id="d626e-116">The following example uses the `Where` method to find orders that were made after December 1, 2003 and then uses the `order.SalesOrderDetail` navigation property to get the details for each order.</span></span>  
  
 [!code-csharp[DP L2E Examples#WhereNavProperty_MQ](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Examples/CS/Program.cs#wherenavproperty_mq)]
 [!code-vb[DP L2E Examples#WhereNavProperty_MQ](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Examples/VB/Module1.vb#wherenavproperty_mq)]  
  
## <a name="wherecontains"></a><span data-ttu-id="d626e-117">Where…Contains</span><span class="sxs-lookup"><span data-stu-id="d626e-117">Where…Contains</span></span>  
  
### <a name="example"></a><span data-ttu-id="d626e-118">Exemplo</span><span class="sxs-lookup"><span data-stu-id="d626e-118">Example</span></span>  
 <span data-ttu-id="d626e-119">O exemplo a seguir usa uma matriz como parte de uma cláusula `Where…Contains` para localizar todos os produtos que têm um `ProductModelID` que coincide com um valor na matriz.</span><span class="sxs-lookup"><span data-stu-id="d626e-119">The following example uses an array as part of a `Where…Contains` clause to find all products that have a `ProductModelID` that matches a value in the array.</span></span>  
  
 [!code-csharp[DP L2E ArraysAndListsInQueries#3](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp l2e arraysandlistsinqueries/cs/program.cs#3)]
 [!code-vb[DP L2E ArraysAndListsInQueries#3](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp l2e arraysandlistsinqueries/vb/module1.vb#3)]  
  
> [!NOTE]
>  <span data-ttu-id="d626e-120">Como parte do predicado em uma cláusula `Where…Contains`, você pode usar um <xref:System.Array>, <xref:System.Collections.Generic.List%601> ou uma coleção de qualquer tipo que implemente a interface de <xref:System.Collections.Generic.IEnumerable%601>.</span><span class="sxs-lookup"><span data-stu-id="d626e-120">As part of the predicate in a `Where…Contains` clause, you can use an <xref:System.Array>, a <xref:System.Collections.Generic.List%601>, or a collection of any type that implements the <xref:System.Collections.Generic.IEnumerable%601> interface.</span></span> <span data-ttu-id="d626e-121">Você também pode declarar e inicializar uma coleção em uma consulta LINQ to Entities.</span><span class="sxs-lookup"><span data-stu-id="d626e-121">You can also declare and initialize a collection within a LINQ to Entities query.</span></span> <span data-ttu-id="d626e-122">Consulte o próximo exemplo para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="d626e-122">See the next example for more information.</span></span>  
  
### <a name="example"></a><span data-ttu-id="d626e-123">Exemplo</span><span class="sxs-lookup"><span data-stu-id="d626e-123">Example</span></span>  
 <span data-ttu-id="d626e-124">O exemplo a seguir declara e inicializa matrizes em uma cláusula `Where…Contains` para localizar todos os produtos que têm um `ProductModelID` ou um `Size` que coincide com um valor nas matrizes.</span><span class="sxs-lookup"><span data-stu-id="d626e-124">The following example declares and initializes arrays in a `Where…Contains` clause to find all products that have a `ProductModelID` or a `Size` that matches a value in the arrays.</span></span>  
  
 [!code-csharp[DP L2E ArraysAndListsInQueries#4](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp l2e arraysandlistsinqueries/cs/program.cs#4)]
 [!code-vb[DP L2E ArraysAndListsInQueries#4](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp l2e arraysandlistsinqueries/vb/module1.vb#4)]  
  
## <a name="see-also"></a><span data-ttu-id="d626e-125">Consulte também</span><span class="sxs-lookup"><span data-stu-id="d626e-125">See Also</span></span>  
 [<span data-ttu-id="d626e-126">Consultas no LINQ to Entities</span><span class="sxs-lookup"><span data-stu-id="d626e-126">Queries in LINQ to Entities</span></span>](../../../../../../docs/framework/data/adonet/ef/language-reference/queries-in-linq-to-entities.md)