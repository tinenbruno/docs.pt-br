---
title: "Serializando um XmlReader (chamada XSLT) (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/03/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
ms.assetid: 8b64f95a-e8f6-40f7-99f9-a8002c63af96
caps.latest.revision: 3
caps.handback.revision: 3
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Serializando um XmlReader (chamada XSLT) (Visual Basic)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

Quando você usa o <xref:System.Xml?displayProperty=fullName> os recursos de interoperabilidade [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)], você pode usar <xref:System.Xml.Linq.XNode.CreateReader%2A> para criar um <xref:System.Xml.XmlReader>. O módulo que lê a partir dessa <xref:System.Xml.XmlReader> lê os nós da árvore XML e processá\-las adequadamente.  
  
## Chamar uma transformação XSLT  
 Um uso possível para esse método é ao chamar uma transformação XSLT. Você pode criar uma árvore XML, criar um <xref:System.Xml.XmlReader> da árvore XML, crie um novo documento e, em seguida, criar um <xref:System.Xml.XmlWriter> para gravar no novo documento. Em seguida, você pode chamar a transformação XSLT, passando <xref:System.Xml.XmlReader> e <xref:System.Xml.XmlWriter>. Depois que a transformação for concluída com êxito, a nova árvore XML é preenchida com os resultados da transformação.  
  
```vb  
Dim xslMarkup As XDocument = _  
    <?xml version='1.0'?>  
    <xsl:stylesheet xmlns:xsl='http://www.w3.org/1999/XSL/Transform' version='1.0'>  
        <xsl:template match='/Parent'>  
            <Root>  
                <C1>  
                    <xsl:value-of select='Child1'/>  
                </C1>  
                <C2>  
                    <xsl:value-of select='Child2'/>  
                </C2>  
            </Root>  
        </xsl:template>  
    </xsl:stylesheet>  
  
Dim xmlTree As XDocument = _  
    <?xml version='1.0'?>  
    <Parent>  
        <Child1>Child1 data</Child1>  
        <Child2>Child2 data</Child2>  
    </Parent>  
  
Dim newTree As XDocument = New XDocument()  
Using writer As XmlWriter = newTree.CreateWriter()  
    ' Load the style sheet.  
    Dim xslt As XslCompiledTransform = New XslCompiledTransform()  
    xslt.Load(xslMarkup.CreateReader())  
  
    ' Execute the transformation and output the results to a writer.  
    xslt.Transform(xmlTree.CreateReader(), writer)  
End Using  
  
Console.WriteLine(newTree)  
```  
  
 Este exemplo produz a seguinte saída:  
  
```xml  
<Root>  
  <C1>Child1 data</C1>  
  <C2>Child2 data</C2>  
</Root>  
```  
  
## Consulte também  
 [Serializando árvores XML \(Visual Basic\)](../../../../visual-basic/programming-guide/concepts/linq/serializing-xml-trees.md)