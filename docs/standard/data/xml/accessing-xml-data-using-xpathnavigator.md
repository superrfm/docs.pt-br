---
title: Acessando dados XML usando XPathNavigator
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-standard
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c57b46e6-5c77-408f-bc4e-67a5dcc9cc05
caps.latest.revision: "2"
author: mairaw
ms.author: mairaw
manager: wpickett
ms.openlocfilehash: 27f5bccc2ab5f229e8b726b3bff18ea7a590f5c0
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="accessing-xml-data-using-xpathnavigator"></a><span data-ttu-id="cc83f-102">Acessando dados XML usando XPathNavigator</span><span class="sxs-lookup"><span data-stu-id="cc83f-102">Accessing XML Data using XPathNavigator</span></span>
<span data-ttu-id="cc83f-103">A classe de <xref:System.Xml.XPath.XPathNavigator> fornece métodos para navegar, nós dados XML do extrair e para acessar dados fortemente tipados XML em um objeto de <xref:System.Xml.XPath.XPathDocument> ou de <xref:System.Xml.XmlDocument> .</span><span class="sxs-lookup"><span data-stu-id="cc83f-103">The <xref:System.Xml.XPath.XPathNavigator> class provides methods to navigate nodes, extract XML data and access strongly typed XML data in an <xref:System.Xml.XPath.XPathDocument> or <xref:System.Xml.XmlDocument> object.</span></span>  
  
## <a name="in-this-section"></a><span data-ttu-id="cc83f-104">Nesta seção</span><span class="sxs-lookup"><span data-stu-id="cc83f-104">In This Section</span></span>  
 [<span data-ttu-id="cc83f-105">Navegação do nó usando XPathNavigator</span><span class="sxs-lookup"><span data-stu-id="cc83f-105">Node Set Navigation Using XPathNavigator</span></span>](../../../../docs/standard/data/xml/node-set-navigation-using-xpathnavigator.md)  
 <span data-ttu-id="cc83f-106">Descreve os métodos definidos de navegação do nó da classe de <xref:System.Xml.XPath.XPathNavigator> usada para navegar nós em um objeto de <xref:System.Xml.XPath.XPathDocument> ou de <xref:System.Xml.XmlDocument> .</span><span class="sxs-lookup"><span data-stu-id="cc83f-106">Describes the node set navigation methods of the <xref:System.Xml.XPath.XPathNavigator> class used to navigate nodes in an <xref:System.Xml.XPath.XPathDocument> or <xref:System.Xml.XmlDocument> object.</span></span>  
  
 [<span data-ttu-id="cc83f-107">Atributo e navegação do nó de Namespace usando XPathNavigator</span><span class="sxs-lookup"><span data-stu-id="cc83f-107">Attribute and Namespace Node Navigation Using XPathNavigator</span></span>](../../../../docs/standard/data/xml/attribute-and-namespace-node-navigation-using-xpathnavigator.md)  
 <span data-ttu-id="cc83f-108">Descreve os métodos de navegação do nó de atributo e do namespace da classe de <xref:System.Xml.XPath.XPathNavigator> .</span><span class="sxs-lookup"><span data-stu-id="cc83f-108">Describes the attribute and namespace node navigation methods of the <xref:System.Xml.XPath.XPathNavigator> class.</span></span>  
  
 [<span data-ttu-id="cc83f-109">Extrair dados XML usando XPathNavigator</span><span class="sxs-lookup"><span data-stu-id="cc83f-109">Extract XML Data Using XPathNavigator</span></span>](../../../../docs/standard/data/xml/extract-xml-data-using-xpathnavigator.md)  
 <span data-ttu-id="cc83f-110">Descreve os vários métodos de extrair dados XML de um objeto de <xref:System.Xml.XPath.XPathDocument> ou de <xref:System.Xml.XmlDocument> .</span><span class="sxs-lookup"><span data-stu-id="cc83f-110">Describes the various methods of extracting XML data from an <xref:System.Xml.XPath.XPathDocument> or <xref:System.Xml.XmlDocument> object.</span></span>  
  
 [<span data-ttu-id="cc83f-111">Acessando dados XML usando XPathNavigator fortemente tipados</span><span class="sxs-lookup"><span data-stu-id="cc83f-111">Accessing Strongly Typed XML Data Using XPathNavigator</span></span>](../../../../docs/standard/data/xml/accessing-strongly-typed-xml-data-using-xpathnavigator.md)  
 <span data-ttu-id="cc83f-112">Descreve acessar dados fortemente tipados XML em um objeto de <xref:System.Xml.XPath.XPathDocument> ou de <xref:System.Xml.XmlDocument> usando a classe de <xref:System.Xml.XPath.XPathNavigator> .</span><span class="sxs-lookup"><span data-stu-id="cc83f-112">Describes accessing strongly-typed XML data in an <xref:System.Xml.XPath.XPathDocument> or <xref:System.Xml.XmlDocument> object using the <xref:System.Xml.XPath.XPathNavigator> class.</span></span>  
  
 [<span data-ttu-id="cc83f-113">Funções e variáveis definidas pelo usuário</span><span class="sxs-lookup"><span data-stu-id="cc83f-113">User Defined Functions and Variables</span></span>](../../../../docs/standard/data/xml/user-defined-functions-and-variables.md)  
 <span data-ttu-id="cc83f-114">Descreve implementar uma classe personalizada de <xref:System.Xml.Xsl.XsltContext> junto com as interfaces <xref:System.Xml.Xsl.IXsltContextFunction> e <xref:System.Xml.Xsl.IXsltContextVariable> que suportam funções e variáveis de extensão.</span><span class="sxs-lookup"><span data-stu-id="cc83f-114">Describes implementing a custom <xref:System.Xml.Xsl.XsltContext> class along with the interfaces <xref:System.Xml.Xsl.IXsltContextFunction> and <xref:System.Xml.Xsl.IXsltContextVariable> that support extension functions and variables.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="cc83f-115">Consulte também</span><span class="sxs-lookup"><span data-stu-id="cc83f-115">See Also</span></span>  
 <xref:System.Xml.XmlDocument>  
 <xref:System.Xml.XPath.XPathDocument>  
 <xref:System.Xml.XPath.XPathNavigator>  
 [<span data-ttu-id="cc83f-116">Processar dados XML usando o modelo de dados XPath</span><span class="sxs-lookup"><span data-stu-id="cc83f-116">Process XML Data Using the XPath Data Model</span></span>](../../../../docs/standard/data/xml/process-xml-data-using-the-xpath-data-model.md)  
 [<span data-ttu-id="cc83f-117">Lendo dados XML usando XPathDocument e XmlDocument</span><span class="sxs-lookup"><span data-stu-id="cc83f-117">Reading XML Data using XPathDocument and XmlDocument</span></span>](../../../../docs/standard/data/xml/reading-xml-data-using-xpathdocument-and-xmldocument.md)  
 [<span data-ttu-id="cc83f-118">Selecionando, avaliando e correspondente de dados XML usando XPathNavigator</span><span class="sxs-lookup"><span data-stu-id="cc83f-118">Selecting, Evaluating and Matching XML Data using XPathNavigator</span></span>](../../../../docs/standard/data/xml/selecting-evaluating-and-matching-xml-data-using-xpathnavigator.md)  
 [<span data-ttu-id="cc83f-119">Editando dados XML usando XPathNavigator</span><span class="sxs-lookup"><span data-stu-id="cc83f-119">Editing XML Data using XPathNavigator</span></span>](../../../../docs/standard/data/xml/editing-xml-data-using-xpathnavigator.md)  
 [<span data-ttu-id="cc83f-120">Validação de esquema usando XPathNavigator</span><span class="sxs-lookup"><span data-stu-id="cc83f-120">Schema Validation using XPathNavigator</span></span>](../../../../docs/standard/data/xml/schema-validation-using-xpathnavigator.md)