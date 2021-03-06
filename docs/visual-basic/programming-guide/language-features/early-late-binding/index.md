---
title: "Associação inicial e tardia (Visual Basic) | Microsoft Docs"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- early binding
- objects [Visual Basic], late-bound
- objects [Visual Basic], early-bound
- objects [Visual Basic], late bound
- early binding, Visual Basic compiler
- binding, late and early
- objects [Visual Basic], early bound
- Visual Basic compiler, early and late binding
- late binding
- late binding, Visual Basic compiler
ms.assetid: d6ff7f1e-b94f-4205-ab8d-5cfa91758724
caps.latest.revision: 10
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 157e1000c30c688ac489d468dcaf9f93b8934002
ms.lasthandoff: 03/13/2017

---
# <a name="early-and-late-binding-visual-basic"></a>Associação antecipada e tardia (Visual Basic)
O compilador [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] executa um processo chamado `binding` quando um objeto é atribuído a uma variável de objeto. Um objeto é *associado inicialmente* quando ele é atribuído a uma variável declarada como de um tipo de objeto específico. Os objetos de associação inicial permitem que o compilador aloque memória e execute outras otimizações antes que um aplicativo seja executado. Por exemplo, o seguinte fragmento de código declara uma variável para ser do tipo <xref:System.IO.FileStream>:  
  
 [!code-vb[VbVbalrOOP#90](../../../../visual-basic/misc/codesnippet/VisualBasic/early-and-late-binding_1.vb)]  
  
 Como <xref:System.IO.FileStream>é um tipo de objeto específico, a instância atribuída a `FS` é a associação inicial.  
  
 Por outro lado, um objeto *associado tardiamente* quando ele é atribuído a uma variável declarada para ser do tipo `Object`. Objetos desse tipo podem conter referências a qualquer objeto, mas têm muitas das vantagens de objetos de associação inicial. Por exemplo, o fragmento de código a seguir declara uma variável de objeto para conter um objeto retornado pela função `CreateObject`:  
  
 [!code-vb[VbVbalrOOP#91](../../../../visual-basic/misc/codesnippet/VisualBasic/early-and-late-binding_2.vb)]  
  
## <a name="advantages-of-early-binding"></a>Vantagens da associação inicial  
 Você deve usar objetos associação inicial sempre que possível, pois eles permitem que o compilador faça otimizações importantes que resultam em aplicativos mais eficientes. Os objetos de associação inicial são significativamente mais rápidos do que objetos de associação tardia e tornam seu código mais fácil de ler e manter informando exatamente quais tipos de objetos estão sendo usados. Outra vantagem da associação inicial é que ela permite que recursos úteis, como a conclusão de código automática e ajuda dinâmica, pois o IDE (ambiente de desenvolvimento integrado) [!INCLUDE[vsprvs](../../../../csharp/includes/vsprvs_md.md)] pode determinar exatamente com qual tipo de objeto você está trabalhando conforme você edita o código. A associação inicial reduz o número e a gravidade dos erros em tempo de execução porque ela permite que o compilador relate erros quando um programa é compilado.  
  
> [!NOTE]
>  A associação tardia só pode ser usada para acessar membros de tipo que são declarados como `Public`. Acessando membros declarados como `Friend` ou `Protected Friend` resulta em um erro em tempo de execução.  
  
## <a name="see-also"></a>Consulte também  
 <xref:Microsoft.VisualBasic.Interaction.CreateObject%2A>   
 [Tempo de vida do objeto: como os objetos são criados e destruídos](../../../../visual-basic/programming-guide/language-features/objects-and-classes/object-lifetime-how-objects-are-created-and-destroyed.md)   
 [Tipo de Dados Object](../../../../visual-basic/language-reference/data-types/object-data-type.md)
