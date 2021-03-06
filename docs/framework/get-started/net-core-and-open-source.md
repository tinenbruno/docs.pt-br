---
title: .NET Core e software livre | Microsoft Docs
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e6bd4655-ce37-4003-8462-468a6fe2c40f
caps.latest.revision: 8
author: mairaw
ms.author: mairaw
manager: wpickett
translationtype: Human Translation
ms.sourcegitcommit: 9f5b8ebb69c9206ff90b05e748c64d29d82f7a16
ms.openlocfilehash: 54bade1b6e310db37537102a1625a76e11e136a7
ms.lasthandoff: 04/18/2017

---
# <a name="net-core-and-open-source"></a>.NET Core e software livre
Este tópico fornece uma breve visão geral sobre o que é o .NET Core e mostra como você pode encontrar mais informações. Para obter a lista completa de tópicos sobre o .NET Core, visite o [Site de documentação do .NET Core](https://docs.microsoft.com/en-us/dotnet/articles/core/index)  
  
<a name="BKMK_WhatisNETCore"></a>   
## <a name="what-is-net-core"></a>O que é o .NET Core?  
 .NET Core é uma implementação de software livre, modular, de plataforma cruzada e para fins gerais da Plataforma .NET. Ele contém muitas das mesmas APIs do .NET Framework (mas o .NET Core é um conjunto menor) e inclui componentes de tempo de execução, estrutura, compilador e ferramentas que oferecem suporte a vários sistemas operacionais e destinos de chip. A implementação do .NET Core foi conduzida principalmente por cargas de trabalho ASP.NET Core, mas também pela necessidade e desejo de ter um tempo de execução mais moderno. Ele pode ser usado em cenários de dispositivo, nuvem e IoT/incorporado.  
  
 Para começar a usar o .NET Core, visite a [Home page do .NET Core](https://www.microsoft.com/net/core).  
  
 Estas são as principais características do .NET Core:  
  
-   **Plataforma cruzada:** o .NET Core fornece uma funcionalidade essencial para implementação de recursos de aplicativo necessários, e reutilização desse código independentemente de seu destino de plataforma. No momento, ele oferece suporte aos três principais sistemas operacionais (SO): Windows, Linux e macOS. Você pode escrever aplicativos e bibliotecas que são executados sem modificações em sistemas operacionais com suporte. Para ver a lista de sistemas operacionais com suporte, visite [Roteiro do .NET Core](https://github.com/dotnet/core/blob/master/roadmap.md) .  
  
-   **Software livre:** o .NET Core é um dos muitos projetos sob a administração do [.NET Foundation](http://www.dotnetfoundation.org/) e está disponível no [GitHub](https://github.com/).  Ter o .NET Core como um projeto de código-fonte aberto promove um processo de desenvolvimento mais transparente e uma comunidade ativa e dedicada.  
  
-   **Implantação flexível:** há duas maneiras de implantar seu aplicativo: implantação dependente da estrutura ou implantação independente. Com a implantação dependente da estrutura, apenas as dependências de seu aplicativo e de terceiros serão instaladas, e seu aplicativo dependerá da presença de uma versão de todo o sistema do .NET Core.  Com a implantação independente, a versão do .NET Core usada para compilar seu aplicativo também será implantada junto com as dependências de seu aplicativo e de terceiros, e poderá ser executada lado a lado com outras versões.    Para saber mais, confira [Implantação de aplicativos .NET Core](https://docs.microsoft.com/en-us/dotnet/articles/core/deploying/index).  
  
-   **Modular:** o .NET Core é modular, pois ele é lançado por meio do NuGet em pacotes menores de assembly. Em vez de um grande assembly contendo a maior parte da funcionalidade principal, o .NET Core é disponibilizado como pacotes menores centrados no recurso. Isso permite um modelo de desenvolvimento mais ágil para nós, e permite a otimização de seu aplicativo a fim de incluir apenas os pacotes do NuGet necessários. Os benefícios de uma área de superfície menor do aplicativo incluem segurança mais rigorosa, manutenção reduzida, desempenho aprimorado e redução dos custos em um modelo de pagamento “pague pelo que usar”.  
  
## <a name="the-net-core-platform"></a>A plataforma do .NET Core  
 A plataforma do .NET Core é composta por vários componentes, incluindo os compiladores gerenciados, o tempo de execução, as bibliotecas de classes base e vários modelos de aplicativo, como o ASP.NET Core. Saiba mais sobre os diferentes componentes e envolva-se visitando os seguintes repositórios do [GitHub](https://github.com/):  
  
-   [.NET Core](https://github.com/dotnet/core)  
  
-   [CoreFX - bibliotecas fundamentais do .NET Core](https://github.com/dotnet/corefx)  
  
-   [CoreCLR - Tempo de execução do .NET Core](https://github.com/dotnet/coreclr)  
  
-   [CLI - Ferramentas da interface de linha de comando do .NET Core](https://github.com/dotnet/cli)  
  
-   [Roslyn - Plataforma do Compilador .NET](https://github.com/dotnet/roslyn)  
  
-   [ASP.NET Core](https://github.com/aspnet/home)  
  
## <a name="see-also"></a>Consulte também  
 [Home page do .NET Core](https://www.microsoft.com/net/core)   
 [Site de documentação do .NET Core](https://docs.microsoft.com/en-us/dotnet/articles/core/index)   
 [Documentação do ASP.NET Core](https://docs.asp.net/)
