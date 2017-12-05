---
title: Inferindo esquemas de documentos XML
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-standard
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- csharp
- vb
- cpp
ms.assetid: f3d97d53-614d-4a04-a174-87965b7405f6
caps.latest.revision: "2"
author: mairaw
ms.author: mairaw
manager: wpickett
ms.openlocfilehash: aa4d6d2758392fc48969b08db30b91bdfe0eeaa1
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="inferring-schemas-from-xml-documents"></a><span data-ttu-id="259d3-102">Inferindo esquemas de documentos XML</span><span class="sxs-lookup"><span data-stu-id="259d3-102">Inferring Schemas from XML Documents</span></span>
<span data-ttu-id="259d3-103">Este tópico descreve como usar a classe de <xref:System.Xml.Schema.XmlSchemaInference> para inferir um esquema de linguagem de definição de esquema XML (XSD) da estrutura de um documento XML.</span><span class="sxs-lookup"><span data-stu-id="259d3-103">This topic describes how to use the <xref:System.Xml.Schema.XmlSchemaInference> class to infer an XML Schema definition language (XSD) schema from the structure of an XML document.</span></span>  
  
## <a name="the-schema-inference-process"></a><span data-ttu-id="259d3-104">O processo de inferência de esquema</span><span class="sxs-lookup"><span data-stu-id="259d3-104">The Schema Inference Process</span></span>  
 <span data-ttu-id="259d3-105">A classe de <xref:System.Xml.Schema.XmlSchemaInference> do espaço de <xref:System.Xml.Schema?displayProperty=nameWithType> é usada para gerar um ou vários esquemas do idioma da definição de esquema XML (XSD) da estrutura de um documento XML.</span><span class="sxs-lookup"><span data-stu-id="259d3-105">The <xref:System.Xml.Schema.XmlSchemaInference> class of the <xref:System.Xml.Schema?displayProperty=nameWithType> namespace is used to generate one or more XML Schema definition language (XSD) schemas from the structure of an XML document.</span></span> <span data-ttu-id="259d3-106">Os esquemas gerados podem ser usados para validar o documento XML original.</span><span class="sxs-lookup"><span data-stu-id="259d3-106">The generated schemas may be used to validate the original XML document.</span></span>  
  
 <span data-ttu-id="259d3-107">Como um documento XML é processado pela classe de <xref:System.Xml.Schema.XmlSchemaInference> , a classe de <xref:System.Xml.Schema.XmlSchemaInference> fazer suposições sobre os componentes do esquema que descrevem os elementos e atributos no documento XML.</span><span class="sxs-lookup"><span data-stu-id="259d3-107">As an XML document is processed by the <xref:System.Xml.Schema.XmlSchemaInference> class, the <xref:System.Xml.Schema.XmlSchemaInference> class makes assumptions about the schema components that describe the elements and attributes in the XML document.</span></span> <span data-ttu-id="259d3-108">A classe de <xref:System.Xml.Schema.XmlSchemaInference> também infere componentes do esquema de uma maneira restrito inferindo o tipo mais restritivo para um elemento ou atributo específico.</span><span class="sxs-lookup"><span data-stu-id="259d3-108">The <xref:System.Xml.Schema.XmlSchemaInference> class also infers schema components in a constrained way by inferring the most restrictive type for a particular element or attribute.</span></span> <span data-ttu-id="259d3-109">Como obter mais informações sobre o documento XML são coletadas, essas restrições são afrouxadas inferindo tipos menos restritivos.</span><span class="sxs-lookup"><span data-stu-id="259d3-109">As more information about the XML document is gathered, these constraints are loosened by inferring less restrictive types.</span></span> <span data-ttu-id="259d3-110">Tipo menos restritivo que pode ser inferido é `xs:string`.</span><span class="sxs-lookup"><span data-stu-id="259d3-110">The least restrictive type that can be inferred is `xs:string`.</span></span>  
  
 <span data-ttu-id="259d3-111">Veja, por exemplo, a seguinte parte de um documento XML.</span><span class="sxs-lookup"><span data-stu-id="259d3-111">Take, for example, the following piece of an XML document.</span></span>  
  
```xml  
<parent attribute1="6">  
    <child>One</child>  
    <child>Two</child>  
</parent>  
<parent attribute1="A">  
```  
  
 <span data-ttu-id="259d3-112">No exemplo anterior, quando o atributo de `attribute1` é encontrado com um valor de `6` pelo processo de <xref:System.Xml.Schema.XmlSchemaInference> , é assumido ser do tipo `xs:unsignedByte`.</span><span class="sxs-lookup"><span data-stu-id="259d3-112">In the example above, when the `attribute1` attribute is encountered with a value of `6` by the <xref:System.Xml.Schema.XmlSchemaInference> process, it is assumed to be of type `xs:unsignedByte`.</span></span> <span data-ttu-id="259d3-113">Quando o segundo elemento de `parent` é encontrado pelo processo de <xref:System.Xml.Schema.XmlSchemaInference> , a restrição está afrouxada alterando tipo a `xs:string` como o valor do atributo de `attribute1` agora é `A`.</span><span class="sxs-lookup"><span data-stu-id="259d3-113">When the second `parent` element is encountered by the <xref:System.Xml.Schema.XmlSchemaInference> process, the constraint is loosened by modifying the type to `xs:string` because the value of the `attribute1` attribute is now `A`.</span></span> <span data-ttu-id="259d3-114">Da mesma forma, o atributo de `minOccurs` para todos os elementos de `child` inferidos no esquema é afrouxado a `minOccurs="0"` porque o segundo elemento pai não tiver nenhum elemento filho.</span><span class="sxs-lookup"><span data-stu-id="259d3-114">Similarly, the `minOccurs` attribute for all the `child` elements inferred in the schema are loosened to `minOccurs="0"` because the second parent element has no child elements.</span></span>  
  
## <a name="inferring-schemas-from-xml-documents"></a><span data-ttu-id="259d3-115">Inferindo esquemas de documentos XML</span><span class="sxs-lookup"><span data-stu-id="259d3-115">Inferring Schemas from XML Documents</span></span>  
 <span data-ttu-id="259d3-116">A classe de <xref:System.Xml.Schema.XmlSchemaInference> usa dois métodos sobrecarregados de <xref:System.Xml.Schema.XmlSchemaInference.InferSchema%2A> para inferir um esquema de um documento XML.</span><span class="sxs-lookup"><span data-stu-id="259d3-116">The <xref:System.Xml.Schema.XmlSchemaInference> class uses two overloaded <xref:System.Xml.Schema.XmlSchemaInference.InferSchema%2A> methods to infer a schema from an XML document.</span></span>  
  
 <span data-ttu-id="259d3-117">O primeiro método de <xref:System.Xml.Schema.XmlSchemaInference.InferSchema%2A?displayProperty=nameWithType> é usado para criar um esquema com base em um documento XML.</span><span class="sxs-lookup"><span data-stu-id="259d3-117">The first <xref:System.Xml.Schema.XmlSchemaInference.InferSchema%2A?displayProperty=nameWithType> method is used to create a schema based on an XML document.</span></span> <span data-ttu-id="259d3-118">O segundo método de <xref:System.Xml.Schema.XmlSchemaInference.InferSchema%2A?displayProperty=nameWithType> é usado para inferir um esquema que descreve vários documentos XML.</span><span class="sxs-lookup"><span data-stu-id="259d3-118">The second <xref:System.Xml.Schema.XmlSchemaInference.InferSchema%2A?displayProperty=nameWithType> method is used to infer a schema that describes multiple XML documents.</span></span> <span data-ttu-id="259d3-119">Por exemplo, você pode alimentar vários documentos XML para o método de <xref:System.Xml.Schema.XmlSchemaInference.InferSchema%2A?displayProperty=nameWithType> um de cada vez para gerar um esquema que descreve o conjunto de documentos XML.</span><span class="sxs-lookup"><span data-stu-id="259d3-119">For example, you can feed multiple XML documents to the <xref:System.Xml.Schema.XmlSchemaInference.InferSchema%2A?displayProperty=nameWithType> method one at a time to produce a schema that describes the entire set of XML documents.</span></span>  
  
 <span data-ttu-id="259d3-120">O primeiro método de <xref:System.Xml.Schema.XmlSchemaInference.InferSchema%2A?displayProperty=nameWithType> infere um esquema de um documento XML contido em um objeto de <xref:System.Xml.XmlReader> , e retorna um objeto de <xref:System.Xml.Schema.XmlSchemaSet> que contém o esquema inferido.</span><span class="sxs-lookup"><span data-stu-id="259d3-120">The first <xref:System.Xml.Schema.XmlSchemaInference.InferSchema%2A?displayProperty=nameWithType> method infers a schema from an XML document contained in an <xref:System.Xml.XmlReader> object, and returns an <xref:System.Xml.Schema.XmlSchemaSet> object containing the inferred schema.</span></span> <span data-ttu-id="259d3-121">O segundo método de <xref:System.Xml.Schema.XmlSchemaInference.InferSchema%2A?displayProperty=nameWithType> procura um objeto de <xref:System.Xml.Schema.XmlSchemaSet> por um esquema com a mesma namespace de destino que o documento XML contido no objeto de <xref:System.Xml.XmlReader> , refinar o esquema existente, e retorna um objeto de <xref:System.Xml.Schema.XmlSchemaSet> que contém o esquema inferido.</span><span class="sxs-lookup"><span data-stu-id="259d3-121">The second <xref:System.Xml.Schema.XmlSchemaInference.InferSchema%2A?displayProperty=nameWithType> method searches an <xref:System.Xml.Schema.XmlSchemaSet> object for a schema with the same target namespace as the XML document contained in the <xref:System.Xml.XmlReader> object, refines the existing schema, and returns an <xref:System.Xml.Schema.XmlSchemaSet> object containing the inferred schema.</span></span>  
  
 <span data-ttu-id="259d3-122">As alterações feitas ao esquema mais aguçado são baseadas na nova estrutura encontrada no documento XML.</span><span class="sxs-lookup"><span data-stu-id="259d3-122">The changes made to the refined schema are based on new structure found in the XML document.</span></span> <span data-ttu-id="259d3-123">Por exemplo, como um documento XML é transmitido, as suposições são feitas sobre os tipos de dados encontrada, e o esquema é criado com base nessas suposições.</span><span class="sxs-lookup"><span data-stu-id="259d3-123">For example, as an XML document is traversed, assumptions are made about the data types found, and the schema is created based on those assumptions.</span></span> <span data-ttu-id="259d3-124">No entanto, se os dados estão localizados em uma segunda passada de inferência suposição que seja diferente do esquema original, é mais aguçado.</span><span class="sxs-lookup"><span data-stu-id="259d3-124">However, if data is encountered on a second inference pass that differs from the original assumption, the schema is refined.</span></span> <span data-ttu-id="259d3-125">O exemplo a seguir ilustra o processo de refinamento.</span><span class="sxs-lookup"><span data-stu-id="259d3-125">The following example illustrates the refinement process.</span></span>  
  
 [!code-cpp[XmlSchemaInferenceExamples#4](../../../../samples/snippets/cpp/VS_Snippets_Data/XmlSchemaInferenceExamples/CPP/XmlSchemaInferenceExamples.cpp#4)]
 [!code-csharp[XmlSchemaInferenceExamples#4](../../../../samples/snippets/csharp/VS_Snippets_Data/XmlSchemaInferenceExamples/CS/XmlSchemaInferenceExamples.cs#4)]
 [!code-vb[XmlSchemaInferenceExamples#4](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XmlSchemaInferenceExamples/VB/XmlSchemaInferenceExamples.vb#4)]  
  
 <span data-ttu-id="259d3-126">O exemplo a seguir utiliza o arquivo, `item1.xml`, como a primeira entrada.</span><span class="sxs-lookup"><span data-stu-id="259d3-126">The example takes the following file, `item1.xml`, as its first input.</span></span>  
  
 [!code-xml[XmlSchemaInferenceExamples#13](../../../../samples/snippets/xml/VS_Snippets_Data/XmlSchemaInferenceExamples/XML/item1.xml#13)]  
  
 <span data-ttu-id="259d3-127">O exemplo usa o arquivo de `item2.xml` como sua entrada segunda:</span><span class="sxs-lookup"><span data-stu-id="259d3-127">The example then takes the `item2.xml` file as its second input:</span></span>  
  
 [!code-xml[XmlSchemaInferenceExamples#14](../../../../samples/snippets/xml/VS_Snippets_Data/XmlSchemaInferenceExamples/XML/item2.xml#14)]  
  
 <span data-ttu-id="259d3-128">Quando o atributo de `productID` está localizado no primeiro documento XML, o valor de `123456789` é assumido ser um tipo de `xs:unsignedInt` .</span><span class="sxs-lookup"><span data-stu-id="259d3-128">When the `productID` attribute is encountered in the first XML document, the value of `123456789` is assumed to be an `xs:unsignedInt` type.</span></span> <span data-ttu-id="259d3-129">No entanto, quando o segundo documento XML é ler e o valor de `A53-246` é encontrado, o tipo de `xs:unsignedInt` não pode mais ser adotado.</span><span class="sxs-lookup"><span data-stu-id="259d3-129">However, when the second XML document is read and the value of `A53-246` is found, the `xs:unsignedInt` type can no longer be assumed.</span></span> <span data-ttu-id="259d3-130">O esquema é mais aguçado e o tipo de `productID` é alterado para `xs:string`.</span><span class="sxs-lookup"><span data-stu-id="259d3-130">The schema is refined and the type of `productID` is changed to `xs:string`.</span></span> <span data-ttu-id="259d3-131">Além disso, o atributo de `minOccurs` para o elemento de `supplierID` é definido como `0`, porque o segundo documento XML não contém elementos de `supplierID` .</span><span class="sxs-lookup"><span data-stu-id="259d3-131">In addition, the `minOccurs` attribute for the `supplierID` element is set to `0`, because the second XML document contains no `supplierID` element.</span></span>  
  
 <span data-ttu-id="259d3-132">O seguinte é o esquema inferido do primeiro documento XML.</span><span class="sxs-lookup"><span data-stu-id="259d3-132">The following is the schema inferred from the first XML document.</span></span>  
  
 [!code-xml[XmlSchemaInferenceExamples#15](../../../../samples/snippets/xml/VS_Snippets_Data/XmlSchemaInferenceExamples/XML/InferSchema1.xml#15)]  
  
 <span data-ttu-id="259d3-133">O seguinte é o esquema inferido do primeiro documento XML, mais aguçado pelo segundo documento XML.</span><span class="sxs-lookup"><span data-stu-id="259d3-133">The following is the schema inferred from the first XML document, refined by the second XML document.</span></span>  
  
 [!code-xml[XmlSchemaInferenceExamples#16](../../../../samples/snippets/xml/VS_Snippets_Data/XmlSchemaInferenceExamples/XML/InferSchema2.xml#16)]  
  
## <a name="inline-schemas"></a><span data-ttu-id="259d3-134">Esquemas in-line</span><span class="sxs-lookup"><span data-stu-id="259d3-134">Inline Schemas</span></span>  
 <span data-ttu-id="259d3-135">Se um esquema de cores do idioma da definição de esquema XML (XSD) é encontrado durante o processo de <xref:System.Xml.Schema.XmlSchemaInference> , <xref:System.Xml.Schema.XmlSchemaInferenceException> é lançada.</span><span class="sxs-lookup"><span data-stu-id="259d3-135">If an inline XML Schema definition language (XSD) schema is encountered during the <xref:System.Xml.Schema.XmlSchemaInference> process, an <xref:System.Xml.Schema.XmlSchemaInferenceException> is thrown.</span></span> <span data-ttu-id="259d3-136">Por exemplo, o seguinte esquema embutido gerencie <xref:System.Xml.Schema.XmlSchemaInferenceException>.</span><span class="sxs-lookup"><span data-stu-id="259d3-136">For example, the following inline schema throws an <xref:System.Xml.Schema.XmlSchemaInferenceException>.</span></span>  
  
```xml  
<root xmlns:ex="http://www.contoso.com" xmlns="http://www.tempuri.org">  
    <xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema" targetNamespace="http://www.contoso.com">  
        <xs:element name="Contoso" type="xs:normalizedString" />  
    </xs:schema>  
    <ex:Contoso>Test</ex:Contoso>  
</root>  
```  
  
## <a name="schemas-that-cannot-be-refined"></a><span data-ttu-id="259d3-137">Esquemas que não podem ser refinados</span><span class="sxs-lookup"><span data-stu-id="259d3-137">Schemas that Cannot be Refined</span></span>  
 <span data-ttu-id="259d3-138">Há construções de Esquema XML do W3C que o processo de <xref:System.Xml.Schema.XmlSchemaInference> do idioma da definição de esquema XML (XSD) não pode manipular se um determinado tipo para refinar e causar uma exceção seja lançada.</span><span class="sxs-lookup"><span data-stu-id="259d3-138">There are W3C XML Schema constructs that the XML Schema definition language (XSD) schema <xref:System.Xml.Schema.XmlSchemaInference> process cannot handle if given a type to refine and cause an exception to be thrown.</span></span> <span data-ttu-id="259d3-139">Como um tipo complexo cujo compositor de nível superior é algo diferente de uma sequência.</span><span class="sxs-lookup"><span data-stu-id="259d3-139">Such as a complex type whose top-level compositor is anything other than a sequence.</span></span> <span data-ttu-id="259d3-140">No modelo de objeto (SOM) do esquema, isso corresponde a <xref:System.Xml.Schema.XmlSchemaComplexType> cuja propriedade de <xref:System.Xml.Schema.XmlSchemaComplexType.Particle%2A> não é uma instância de <xref:System.Xml.Schema.XmlSchemaSequence>.</span><span class="sxs-lookup"><span data-stu-id="259d3-140">In the Schema Object Model (SOM), this corresponds to an <xref:System.Xml.Schema.XmlSchemaComplexType> whose <xref:System.Xml.Schema.XmlSchemaComplexType.Particle%2A> property is not an instance of <xref:System.Xml.Schema.XmlSchemaSequence>.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="259d3-141">Consulte também</span><span class="sxs-lookup"><span data-stu-id="259d3-141">See Also</span></span>  
 <xref:System.Xml.Schema.XmlSchemaInference>  
 <span data-ttu-id="259d3-142">[XML Schema Object Model (SOM)](../../../../docs/standard/data/xml/xml-schema-object-model-som.md) [SOM (Modelo de Objeto de Esquema) XML]</span><span class="sxs-lookup"><span data-stu-id="259d3-142">[XML Schema Object Model (SOM)](../../../../docs/standard/data/xml/xml-schema-object-model-som.md)</span></span>  
 [<span data-ttu-id="259d3-143">Inferindo um esquema XML</span><span class="sxs-lookup"><span data-stu-id="259d3-143">Inferring an XML Schema</span></span>](../../../../docs/standard/data/xml/inferring-an-xml-schema.md)  
 [<span data-ttu-id="259d3-144">Regras para inferir tipos de nó do esquema e estrutura</span><span class="sxs-lookup"><span data-stu-id="259d3-144">Rules for Inferring Schema Node Types and Structure</span></span>](../../../../docs/standard/data/xml/rules-for-inferring-schema-node-types-and-structure.md)  
 [<span data-ttu-id="259d3-145">Regras para inferir tipos simples</span><span class="sxs-lookup"><span data-stu-id="259d3-145">Rules for Inferring Simple Types</span></span>](../../../../docs/standard/data/xml/rules-for-inferring-simple-types.md)