---
title: "Fluxo de controle em programas assíncronos (C#) | Microsoft Docs"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
ms.assetid: fc92b08b-fe1d-4d07-84ab-5192fafe06bb
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: d014ddcdfabae83343de6b1e9338ae38fe2b22d0
ms.lasthandoff: 03/13/2017

---
# <a name="control-flow-in-async-programs-c"></a>Fluxo de controle em programas assíncronos (C#)
Você pode escrever e manter programas assíncronos mais facilmente usando as palavras-chave `async` e `await`. No entanto, os resultados podem surpreendê-lo se você não entender o funcionamento do seu programa. Este tópico rastreia o fluxo de controle por meio de um programa assíncrono simples para mostrar quando o controle se move de um método para o outro e quais informações são transferidas a cada vez.  
  
> [!NOTE]
>  As palavras-chave `async` e `await` foram introduzidas no Visual Studio 2012.  
  
 Em geral, você marca os métodos que contêm código assíncrono com o modificador [async (C#)](../../../../csharp/language-reference/keywords/async.md). Em um método marcado com um modificador assíncrono, você pode usar um operador [await (C#)](../../../../csharp/language-reference/keywords/await.md) para especificar o local em que o método faz uma pausa para esperar pela conclusão de um processo assíncrono que foi chamado. Para obter mais informações, consulte [Programação assíncrona com async e await (C#)](../../../../csharp/programming-guide/concepts/async/index.md).  
  
 O exemplo a seguir usa os métodos assíncronos para baixar o conteúdo de um site especificado como uma cadeia de caracteres e exibir o comprimento da cadeia de caracteres. O exemplo contém os dois métodos a seguir.  
  
-   `startButton_Click`, que chama `AccessTheWebAsync` e exibe o resultado.  
  
-   `AccessTheWebAsync`, que baixa o conteúdo de um site na forma de uma cadeia de caracteres e retorna o comprimento da cadeia de caracteres. `AccessTheWebAsync` usa um método <xref:System.Net.Http.HttpClient> assíncrono, o <xref:System.Net.Http.HttpClient.GetStringAsync%28System.String%29>, para baixar o conteúdo.  
  
 Linhas numeradas de exibição aparecem em pontos estratégicos em todo o programa para ajudá-lo a entender como o programa é executado e explicar o que acontece em cada ponto marcado. As linhas de exibição são rotuladas como "UM"a "SEIS". Os rótulos representam a ordem na qual o programa alcança essas linhas de código.  
  
 O código a seguir mostra uma estrutura de tópicos do programa.  
  
```cs  
  
public partial class MainWindow : Window  
{  
    // . . .  
    private async void startButton_Click(object sender, RoutedEventArgs e)  
    {  
        // ONE  
        Task<int> getLengthTask = AccessTheWebAsync();  
  
        // FOUR  
        int contentLength = await getLengthTask;  
  
        // SIX  
        resultsTextBox.Text +=  
            String.Format("\r\nLength of the downloaded string: {0}.\r\n", contentLength);  
    }  
  
    async Task<int> AccessTheWebAsync()  
    {  
        // TWO  
        HttpClient client = new HttpClient();  
        Task<string> getStringTask =  
            client.GetStringAsync("http://msdn.microsoft.com");  
  
        // THREE                   
        string urlContents = await getStringTask;  
  
        // FIVE  
        return urlContents.Length;  
    }  
}  
  
```  
  
 Cada um dos locais rotulados, "UM"a "SEIS," exibe informações sobre o estado atual do programa. A saída a seguir será produzida.  
  
```  
  
ONE:   Entering startButton_Click.  
           Calling AccessTheWebAsync.  
  
TWO:   Entering AccessTheWebAsync.  
           Calling HttpClient.GetStringAsync.  
  
THREE: Back in AccessTheWebAsync.  
           Task getStringTask is started.  
           About to await getStringTask & return a Task<int> to startButton_Click.  
  
FOUR:  Back in startButton_Click.  
           Task getLengthTask is started.  
           About to await getLengthTask -- no caller to return to.  
  
FIVE:  Back in AccessTheWebAsync.  
           Task getStringTask is complete.  
           Processing the return statement.  
           Exiting from AccessTheWebAsync.  
  
SIX:   Back in startButton_Click.  
           Task getLengthTask is finished.  
           Result from AccessTheWebAsync is stored in contentLength.  
           About to display contentLength and exit.  
  
Length of the downloaded string: 33946.  
```  
  
## <a name="set-up-the-program"></a>Configurar o Programa  
 Você pode baixar o código usado nesse tópico no MSDN ou você mesmo pode criá-lo.  
  
> [!NOTE]
>  Para executar o exemplo, você deve ter o Visual Studio 2012 ou mais recente e o .NET Framework 4.5 ou posterior instalados no seu computador.  
  
### <a name="download-the-program"></a>Baixar o Programa  
 Você pode baixar o aplicativo deste tópico em [Exemplo assíncrono: controlar fluxo em programas assíncronos](http://go.microsoft.com/fwlink/?LinkId=255285). As etapas a seguir abrem e executam o programa.  
  
1.  Descompacte o arquivo baixado e, em seguida, inicie o Visual Studio.  
  
2.  Na barra de menus, escolha **Arquivo**, **Abrir**, **Projeto/Solução**.  
  
3.  Navegue até a pasta que contém o código de exemplo descompactado, abra o arquivo da solução (.sln) e, em seguida, escolha a tecla F5 para compilar e executar o projeto.  
  
### <a name="build-the-program-yourself"></a>Compilar o Programa Sozinho  
 O projeto WPF (Windows Presentation Foundation) a seguir contém o exemplo de código deste tópico.  
  
 Para executar o projeto, realize as seguintes etapas:  
  
1.  Inicie o Visual Studio.  
  
2.  Na barra de menus, escolha **Arquivo**, **Novo**, **Projeto**.  
  
     A caixa de diálogo **Novo Projeto** é aberta.  
  
3.  No painel **Modelos Instalados**, escolha **Visual C#** e, em seguida, escolha **Aplicativo WPF** na lista de tipos de projeto.  
  
4.  Digite `AsyncTracer` como o nome do projeto e, em seguida, escolha o botão **OK**.  
  
     O novo projeto aparece no **Gerenciador de Soluções**.  
  
5.  No Editor do Visual Studio Code, escolha a guia **MainWindow.xaml**.  
  
     Se a guia não estiver visível, abra o menu de atalho para MainWindow.xaml no **Gerenciador de Soluções** e, em seguida, escolha **Exibir Código**.  
  
6.  Na exibição **XAML** de MainWindow.xaml, substitua o código pelo código a seguir.  
  
    ```cs  
    <Window  
            xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"  
            xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"  
            xmlns:d="http://schemas.microsoft.com/expression/blend/2008" xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006" mc:Ignorable="d" x:Class="AsyncTracer.MainWindow"  
            Title="Control Flow Trace" Height="350" Width="592">  
        <Grid>  
            <Button x:Name="startButton" Content="Start  
    " HorizontalAlignment="Left" Margin="250,10,0,0" VerticalAlignment="Top" Width="75" Height="24"  Click="startButton_Click" d:LayoutOverrides="GridBox"/>  
            <TextBox x:Name="resultsTextBox" HorizontalAlignment="Left" TextWrapping="Wrap" VerticalAlignment="Bottom" Width="576" Height="265" FontFamily="Lucida Console" FontSize="10" VerticalScrollBarVisibility="Visible" Grid.ColumnSpan="3"/>  
        </Grid>  
    </Window>  
  
    ```  
  
     Uma janela simples, contendo uma caixa de texto e um botão, aparecerá no modo de exibição de **Design** de MainWindow.xaml.  
  
7.  Adicione uma referência para <xref:System.Net.Http>.  
  
8.  No **Gerenciador de Soluções**, abra o menu de atalho de MainWindow.xaml.cs e, em seguida, escolha **Exibir Código**.  
  
9. Em MainWindow.xaml.cs, substitua o código pelo código a seguir.  
  
    ```cs  
    using System;  
    using System.Collections.Generic;  
    using System.Linq;  
    using System.Text;  
    using System.Threading.Tasks;  
    using System.Windows;  
    using System.Windows.Controls;  
    using System.Windows.Data;  
    using System.Windows.Documents;  
    using System.Windows.Input;  
    using System.Windows.Media;  
    using System.Windows.Media.Imaging;  
    using System.Windows.Navigation;  
    using System.Windows.Shapes;  
  
    // Add a using directive and a reference for System.Net.Http;  
    using System.Net.Http;  
  
    namespace AsyncTracer  
    {  
        public partial class MainWindow : Window  
        {  
            public MainWindow()  
            {  
                InitializeComponent();  
            }  
  
            private async void startButton_Click(object sender, RoutedEventArgs e)  
            {  
                // The display lines in the example lead you through the control shifts.  
                resultsTextBox.Text += "ONE:   Entering startButton_Click.\r\n" +  
                    "           Calling AccessTheWebAsync.\r\n";  
  
                Task<int> getLengthTask = AccessTheWebAsync();  
  
                resultsTextBox.Text += "\r\nFOUR:  Back in startButton_Click.\r\n" +  
                    "           Task getLengthTask is started.\r\n" +  
                    "           About to await getLengthTask -- no caller to return to.\r\n";  
  
                int contentLength = await getLengthTask;  
  
                resultsTextBox.Text += "\r\nSIX:   Back in startButton_Click.\r\n" +  
                    "           Task getLengthTask is finished.\r\n" +  
                    "           Result from AccessTheWebAsync is stored in contentLength.\r\n" +  
                    "           About to display contentLength and exit.\r\n";  
  
                resultsTextBox.Text +=  
                    String.Format("\r\nLength of the downloaded string: {0}.\r\n", contentLength);  
            }  
  
            async Task<int> AccessTheWebAsync()  
            {  
                resultsTextBox.Text += "\r\nTWO:   Entering AccessTheWebAsync.";  
  
                // Declare an HttpClient object.  
                HttpClient client = new HttpClient();  
  
                resultsTextBox.Text += "\r\n           Calling HttpClient.GetStringAsync.\r\n";  
  
                // GetStringAsync returns a Task<string>.   
                Task<string> getStringTask = client.GetStringAsync("http://msdn.microsoft.com");  
  
                resultsTextBox.Text += "\r\nTHREE: Back in AccessTheWebAsync.\r\n" +  
                    "           Task getStringTask is started.";  
  
                // AccessTheWebAsync can continue to work until getStringTask is awaited.  
  
                resultsTextBox.Text +=  
                    "\r\n           About to await getStringTask and return a Task<int> to startButton_Click.\r\n";  
  
                // Retrieve the website contents when task is complete.  
                string urlContents = await getStringTask;  
  
                resultsTextBox.Text += "\r\nFIVE:  Back in AccessTheWebAsync." +  
                    "\r\n           Task getStringTask is complete." +  
                    "\r\n           Processing the return statement." +  
                    "\r\n           Exiting from AccessTheWebAsync.\r\n";  
  
                return urlContents.Length;  
            }  
        }  
    }  
    ```  
  
10. Escolha a tecla F5 para executar o programa e, em seguida, escolha o botão **Iniciar**.  
  
     A saída a seguir deverá aparecer.  
  
    ```  
    ONE:   Entering startButton_Click.  
               Calling AccessTheWebAsync.  
  
    TWO:   Entering AccessTheWebAsync.  
               Calling HttpClient.GetStringAsync.  
  
    THREE: Back in AccessTheWebAsync.  
               Task getStringTask is started.  
               About to await getStringTask & return a Task<int> to startButton_Click.  
  
    FOUR:  Back in startButton_Click.  
               Task getLengthTask is started.  
               About to await getLengthTask -- no caller to return to.  
  
    FIVE:  Back in AccessTheWebAsync.  
               Task getStringTask is complete.  
               Processing the return statement.  
               Exiting from AccessTheWebAsync.  
  
    SIX:   Back in startButton_Click.  
               Task getLengthTask is finished.  
               Result from AccessTheWebAsync is stored in contentLength.  
               About to display contentLength and exit.  
  
    Length of the downloaded string: 33946.  
    ```  
  
## <a name="trace-the-program"></a>Rastrear o Programa  
  
### <a name="steps-one-and-two"></a>Etapas UM e DOIS  
 As duas primeiras linhas de exibição rastreiam o caminho como chamadas `startButton_Click`, `AccessTheWebAsync` e chamadas `AccessTheWebAsync` ao método <xref:System.Net.Http.HttpClient> assíncrono, <xref:System.Net.Http.HttpClient.GetStringAsync%28System.String%29>. A imagem a seguir delineia as chamadas de método a método.  
  
 ![Etapas UM e DOIS](../../../../csharp/programming-guide/concepts/async/media/asynctrace-onetwo.png "AsyncTrace-ONETWO")  
  
 O tipo de retorno de `AccessTheWebAsync` e `client.GetStringAsync` é <xref:System.Threading.Tasks.Task%601>. Para `AccessTheWebAsync`, TResult é um inteiro. Para `GetStringAsync`, TResult é uma cadeia de caracteres. Para obter mais informações sobre tipos de retorno de método assíncrono, consulte [Tipos de retorno assíncronos (C#)](../../../../csharp/programming-guide/concepts/async/async-return-types.md).  
  
 Um método assíncrono de retorno de tarefas retorna uma instância de tarefa, quando o controle volta para o chamador. O controle retorna de um método assíncrono para seu chamador quando um operador `await` é encontrado no método chamado ou quando o método chamado termina. As linhas de exibição rotuladas como "TRÊS"até "SEIS" rastreiam essa parte do processo.  
  
### <a name="step-three"></a>Etapa TRÊS  
 Em `AccessTheWebAsync`, o método assíncrono <xref:System.Net.Http.HttpClient.GetStringAsync%28System.String%29> é chamado para baixar o conteúdo de página da Web de destino. O controle retorna de `client.GetStringAsync` para `AccessTheWebAsync` quando `client.GetStringAsync` retornar.  
  
 O método `client.GetStringAsync` retorna uma tarefa de cadeia de caracteres que é atribuída à variável `getStringTask` em `AccessTheWebAsync`. A linha do programa de exemplo a seguir mostra a chamada à `client.GetStringAsync` e a atribuição.  
  
<CodeContentPlaceHolder>5</CodeContentPlaceHolder>  
 Você pode imaginar a tarefa como uma promessa de `client.GetStringAsync` para eventualmente produzir uma cadeia de caracteres real. Enquanto isso, se `AccessTheWebAsync` tiver trabalho a fazer, que não dependa da cadeia de caracteres prometida de `client.GetStringAsync`, o trabalho poderá continuar enquanto `client.GetStringAsync` aguarda. No exemplo, as seguintes linhas de saída, que são rotuladas "TRÊS", representam a oportunidade para fazer trabalho independente  
  
<CodeContentPlaceHolder>6</CodeContentPlaceHolder>  
 A instrução a seguir suspende o andamento em `AccessTheWebAsync` quando `getStringTask` é aguardado.  
  
<CodeContentPlaceHolder>7</CodeContentPlaceHolder>  
 A imagem a seguir mostra o fluxo de controle de `client.GetStringAsync` para a atribuição ao `getStringTask` e da criação de `getStringTask` para a aplicação de um operador de espera.  
  
 ![Etapa TRÊS](../../../../csharp/programming-guide/concepts/async/media/asynctrace-three.png "AsyncTrace-Three")  
  
 A expressão await suspende `AccessTheWebAsync` até que `client.GetStringAsync` retorne. Enquanto isso, o controle retorna para o chamador de `AccessTheWebAsync`, `startButton_Click`.  
  
> [!NOTE]
>  Normalmente, você aguarda a chamada a um método assíncrono imediatamente. Por exemplo, a atribuição a seguir poderia substituir o código anterior que cria e, em seguida, aguarda `getStringTask`: `string urlContents = await client.GetStringAsync("http://msdn.microsoft.com");`  
>   
>  Neste tópico, o operador await é aplicado posteriormente para acomodar as linhas de saída que marcam o fluxo de controle em todo o programa.  
  
### <a name="step-four"></a>Etapa QUATRO  
 O tipo de retorno declarado de `AccessTheWebAsync` é `Task<int>`. Portanto, quando `AccessTheWebAsync` for suspenso, ele retornará uma tarefa de inteiro para `startButton_Click`. Você deve compreender que a tarefa retornada não é `getStringTask`. A tarefa retornada é uma nova tarefa de um inteiro que representa o que ainda precisa ser feito no método suspenso `AccessTheWebAsync`. A tarefa é uma promessa de `AccessTheWebAsync` para produzir um inteiro quando a tarefa for concluída.  
  
 A instrução a seguir atribui essa tarefa à variável `getLengthTask`.  
  
<CodeContentPlaceHolder>8</CodeContentPlaceHolder>  
 Como em `AccessTheWebAsync`, `startButton_Click` pode continuar com o trabalho que não dependa dos resultados da tarefa assíncrona (`getLengthTask`) até que a tarefa seja aguardada. As seguintes linhas de saída representam esse trabalho.  
  
<CodeContentPlaceHolder>9</CodeContentPlaceHolder>  
 O avanço em `startButton_Click` será suspenso quando `getLengthTask` for aguardada. A seguinte instrução de atribuição suspende `startButton_Click` até que `AccessTheWebAsync` seja concluída.  
  
<CodeContentPlaceHolder>10</CodeContentPlaceHolder>  
 Na ilustração a seguir, as setas mostram o fluxo de controle da expressão await em `AccessTheWebAsync` para a atribuição de um valor para `getLengthTask`, seguido pelo processamento normal de `startButton_Click` até que `getLengthTask` seja aguardada.  
  
 ![Etapa QUATRO](../../../../csharp/programming-guide/concepts/async/media/asynctrace-four.png "AsyncTrace-FOUR")  
  
### <a name="step-five"></a>Etapa CINCO  
 Quando `client.GetStringAsync` sinaliza que está concluído, o processamento em `AccessTheWebAsync` é liberado da suspensão e pode continuar após a instrução await. As seguintes linhas de saída representam a retomada do processamento.  
  
<CodeContentPlaceHolder>11</CodeContentPlaceHolder>  
 O operando da instrução return, `urlContents.Length`, é armazenado na tarefa que `AccessTheWebAsync` retorna. A expressão await recupera esse valor de `getLengthTask` em `startButton_Click`.  
  
 A imagem a seguir mostra a transferência de controle após `client.GetStringAsync` (e `getStringTask`) estarem concluídas.  
  
 ![Etapa CINCO](../../../../csharp/programming-guide/concepts/async/media/asynctrace-five.png "AsyncTrace-FIVE")  
  
 `AccessTheWebAsync` é executado até a conclusão e o controle retorna ao `startButton_Click`, que está aguardando a conclusão.  
  
### <a name="step-six"></a>Etapa SEIS  
 Quando `AccessTheWebAsync` sinaliza que está concluído, o processamento pode continuar após a instrução await em `startButton_Async`. Na verdade, o programa não tem mais nada para fazer.  
  
 As seguintes linhas de saída representam a retomada do processamento em `startButton_Async`:  
  
<CodeContentPlaceHolder>12</CodeContentPlaceHolder>  
 A expressão await recupera de `getLengthTask` o valor inteiro, que é o operando da instrução return em `AccessTheWebAsync`. A instrução a seguir atribui esse valor à variável `contentLength`.  
  
<CodeContentPlaceHolder>13</CodeContentPlaceHolder>  
 A imagem a seguir mostra o retorno do controle de `AccessTheWebAsync` para `startButton_Click`.  
  
 ![Etapa SEIS](../../../../csharp/programming-guide/concepts/async/media/asynctrace-six.png "AsyncTrace-SIX")  
  
## <a name="see-also"></a>Consulte também  
 [Programação assíncrona com async e await (C#)](../../../../csharp/programming-guide/concepts/async/index.md)   
 [Tipos de retorno assíncronos (C#)](../../../../csharp/programming-guide/concepts/async/async-return-types.md)   
 [Passo a passo: acessando a Web usando async e await (C#)](../../../../csharp/programming-guide/concepts/async/walkthrough-accessing-the-web-by-using-async-and-await.md)   
 [Exemplo de assíncrono: fluxo de controle em programas assíncronos (C# e Visual Basic)](http://go.microsoft.com/fwlink/?LinkId=255285)
