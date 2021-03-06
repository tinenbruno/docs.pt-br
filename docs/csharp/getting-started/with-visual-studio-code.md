---
title: "Introdução ao Visual Studio Code | Guia do C#"
description: Saiba como criar e depurar seu primeiro aplicativo .NET Core em C# usando o VS Code.
keywords: "C#, Introdução, Aquisição, Instalação, Visual Studio Code, Plataforma Cruzada"
author: kendrahavens
ms.author: mairaw
ms.date: 03/07/2017
ms.topic: article
ms.prod: .net
ms.technology: devlang-csharp
ms.devlang: csharp
ms.assetid: 76c23597-4cf9-467e-8a47-0c3703ce37e7
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 4550129f4e6f1eeb3521ad7fe3233f2bda49e5c5
ms.lasthandoff: 03/13/2017

---

# <a name="getting-started-with-visual-studio-code"></a>Introdução ao Visual Studio Code

O .NET Core oferece uma plataforma modular e rápida para a criação de aplicativos de servidor que são executados no Windows, Linux e macOS. Use o Visual Studio Code com a extensão do C# para obter uma excelente experiência de edição com suporte completo para IntelliSense em C# (conclusão de código inteligente) e depuração.

## <a name="prerequisites"></a>Pré-requisitos

1. Instalar o [Visual Studio Code](https://code.visualstudio.com/).
2. Instalar o [SDK do .NET Core](https://www.microsoft.com/net/download/core).
3. Instalar a [extensão C#](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp) do Visual Studio Code Marketplace.

## <a name="hello-world"></a>Hello World

Vamos começar com um simples programa "Olá, Mundo" no .NET Core:

1. Abra um projeto:

    * Abra o VS Code.
    * Clique no ícone do Explorer no menu à esquerda e, em seguida, clique em **Abrir Pasta**.
    * Selecione a pasta que você deseja que seu projeto em C# esteja e clique em **Selecionar Pasta**. Para nosso exemplo, vamos criar uma pasta para nosso projeto chamado 'HelloWorld'. 

  ![VSCodeOpenFolder](media/with-visual-studio-code/vscodeopenfolder.png)

    * Como alternativa, você pode selecionar **Arquivo** > **Abrir Pasta** no menu principal para abrir a pasta do projeto.

2. Inicialize um projeto em C#:
    * Abra o Terminal Integrado do VS Code digitando <kbd>CTRL</kbd>+<kbd>\`</kbd> (acento grave).
    * Na janela do terminal, digite `dotnet new console`.
    * Isso cria um arquivo `Program.cs` em sua pasta com um programa simples "Olá, Mundo" já escrito, junto com um arquivo de projeto em C# chamado `HelloWorld.csproj`.

  ![O novo comando dotnet](media/with-visual-studio-code/dotnetnew.png)

3. Resolva os ativos do build:

    * Digite `dotnet restore`. Executar `dotnet restore` fornece acesso a pacotes .NET Core que são necessários para compilar seu projeto.

  ![O comando de restauração dotnet](media/with-visual-studio-code/dotnetrestore.png)

4. Execute o programa "Olá, Mundo":

    * Digite `dotnet run`. 

  ![O comando de execução dotnet](media/with-visual-studio-code/dotnetrun.png)

Você também pode assistir a um tutorial breve em vídeo para obter ajuda na instalação em [Windows](https://channel9.msdn.com/Blogs/dotnet/Get-started-with-VS-Code-using-CSharp-and-NET-Core), [macOS](https://channel9.msdn.com/Blogs/dotnet/Get-started-with-VS-Code-using-CSharp-and-NET-Core-on-MacOS) ou [Linux](https://channel9.msdn.com/Blogs/dotnet/Get-started-with-VS-Code-Csharp-dotnet-Core-Ubuntu).

## <a name="debug"></a>Depurar
1. Abra *Program.cs* clicando nele. A primeira vez que você abrir um arquivo em C# no VS Code, o [OmniSharp](http://www.omnisharp.net/) será carregado no editor.

  ![Abra o arquivo Program.cs](media/with-visual-studio-code/opencs.png)

2. O VS Code solicitará que você adicione os ativos ausentes para compilar e depurar seu aplicativo. Selecione **Sim**. 

  ![Prompt para ativos ausentes](media/with-visual-studio-code/missing-assets.png)

3. Para abrir e exibição Depuração, clique no ícone Depuração no menu do lado esquerdo.

  ![Abra a guia Depurar](media/with-visual-studio-code/opendebug.png)

4. Localize a seta verde na parte superior do painel. Certifique-se que a lista suspensa ao lado tenha `.NET Core Launch (console)` selecionado.

  ![Seleção do .NET Core](media/with-visual-studio-code/selectcore.png)

5. Adicione um ponto de interrupção ao seu projeto clicando na **margem do editor** (no espaço à esquerda dos números de linha no editor) ao lado da linha 9.

  ![Definindo um ponto de interrupção](media/with-visual-studio-code/setbreakpoint.png)

6. Selecione <kbd>F5</kbd> ou a seta verde para iniciar a depuração. O depurador interrompe a execução do programa quando ele atinge o ponto de interrupção definido na etapa anterior.
    * Durante a depuração, você pode exibir as variáveis locais no painel superior esquerdo ou usar o console de depuração.

  ![Executar e depurar](media/with-visual-studio-code/rundebug.png)

7. Selecione a seta verde na parte superior para continuar a depuração ou pressione o quadrado vermelho para parar.

> [!TIP] 
> Para obter mais informações e dicas sobre solução de problemas de depuração do .NET Core com OmniSharp no VS Code, consulte [Instruções para configurar o depurador .NET Core](https://github.com/OmniSharp/omnisharp-vscode/blob/master/debugger.md).

## <a name="see-also"></a>Consulte também
- [Configurando o Visual Studio Code](https://code.visualstudio.com/docs/setup/setup-overview)
- [Depurando no Visual Studio Code](https://code.visualstudio.com/Docs/editor/debugging)

