---
title: "Instruções passo a passo: criar um botão usando XAML"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-wpf
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: buttons [WPF]
ms.assetid: 138c41c4-1759-4bbf-8d77-77031a06a8a0
caps.latest.revision: "13"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 5c5efa9f8787e65d59e1b544632e806bf3fbbc81
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/22/2017
---
# <a name="walkthrough-create-a-button-by-using-xaml"></a>Instruções passo a passo: criar um botão usando XAML
O objetivo deste passo a passo é aprender a criar um botão animado para uso em um aplicativo do [!INCLUDE[TLA#tla_wpf](../../../../includes/tlasharptla-wpf-md.md)]. Este passo a passo usa estilos e um modelo para criar um recurso de botão personalizado que permite a reutilização de código e separação da lógica do botão da declaração do botão. Este passo a passo é escrito inteiramente em [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)].  
  
> [!IMPORTANT]
>  Este passo a passo orienta você pelas etapas para criar o aplicativo, digitando ou copiando e colando o [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] no Microsoft [!INCLUDE[vs_current_short](../../../../includes/vs-current-short-md.md)]. Se você prefere aprender a usar uma ferramenta de design (Microsoft Expression Blend) para criar o mesmo aplicativo, consulte [Criar um botão, usando o Microsoft Expression Blend](../../../../docs/framework/wpf/controls/walkthrough-create-a-button-by-using-microsoft-expression-blend.md).  
  
 A figura a seguir mostra os botões concluídos.  
  
 ![Botões personalizados criados com XAML](../../../../docs/framework/wpf/controls/media/custom-button-animatedbutton-5.gif "custom_button_AnimatedButton_5")  
  
## <a name="create-basic-buttons"></a>Criar botões básicos  
 Vamos começar criando um novo projeto e adicionando alguns botões à janela.  
  
#### <a name="to-create-a-new-wpf-project-and-add-buttons-to-the-window"></a>Para criar um novo projeto WPF e adicionar botões à janela  
  
1.  Inicie o [!INCLUDE[vs_current_short](../../../../includes/vs-current-short-md.md)].  
  
2.  **Criar um novo projeto WPF:** no menu **Arquivo**, aponte para **Novo** e, em seguida, clique em **Projeto**. Encontre o modelo do **Aplicativo do Windows (WPF)** e nomeie o projeto como "AnimatedButton". Isso criará o esqueleto para o aplicativo.  
  
3.  **Adicionar botões padrão básicos:** todos os arquivos necessários para esse passo a passo são fornecidos pelo modelo. Abra o arquivo Window1.xaml, clicando duas vezes nele no Gerenciador de Soluções. Por padrão, há um <xref:System.Windows.Controls.Grid> elemento Window1. Remover o <xref:System.Windows.Controls.Grid> elemento e adicione alguns botões para o [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] página digitando ou copiando e colando o seguinte código realçado para Window1. XAML:  
  
    ```xaml  
    <Window x:Class="AnimatedButton.Window1"  
      xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"  
      xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"  
      Title="AnimatedButton" Height="300" Width="300"   
      Background="Black">   <!-- Buttons arranged vertically inside a StackPanel. -->   <StackPanel HorizontalAlignment="Left">     <Button>Button 1</Button>     <Button>Button 2</Button>     <Button>Button 3</Button>   </StackPanel>  
  
    </Window>  
    ```  
  
     Pressione F5 para executar o aplicativo. Você deverá ver um conjunto de botões parecido com a figura a seguir.  
  
     ![Três botões básicos](../../../../docs/framework/wpf/controls/media/custom-button-animatedbutton-1.gif "custom_button_AnimatedButton_1")  
  
     Agora que você criou os botões básicos, o trabalho no arquivo Window1.xaml está concluído. O restante do passo a passo se concentrará no arquivo app.xaml, definindo estilos e um modelo para os botões.  
  
## <a name="set-basic-properties"></a>Definir propriedades básicas  
 Em seguida, vamos definir algumas propriedades para controlar a aparência e o layout desses botões. Em vez de definir propriedades em cada botão, você usará recursos para definir propriedades de botão para todo o aplicativo. Os recursos de aplicativo são conceitualmente semelhantes à [!INCLUDE[TLA#tla_css](../../../../includes/tlasharptla-css-md.md)] externa para páginas da Web. No entanto, os recursos são muito mais eficientes do que a [!INCLUDE[TLA#tla_css](../../../../includes/tlasharptla-css-md.md)], como você verá no final deste passo a passo. Para saber mais sobre recursos, consulte [Recursos XAML](../../../../docs/framework/wpf/advanced/xaml-resources.md).  
  
#### <a name="to-use-styles-to-set-basic-properties-on-the-buttons"></a>Usar estilos para definir propriedades básicas nos botões  
  
1.  **Definir um bloco Application.Resources:** abra o app.xaml e adicione a seguinte marcação realçada, se ainda não estiver lá:  
  
    ```xaml  
    <Application x:Class="AnimatedButton.App"  
      xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"  
      xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"  
      StartupUri="Window1.xaml"  
      >  
      <Application.Resources>
        <!-- Resources for the entire application can be defined here. -->
      </Application.Resources>  
    </Application>  
    ```  
  
     O escopo do recurso é determinado pelo local em que você define o recurso. A definição de recursos em `Application.Resources` no arquivo app.xaml permite que o recurso seja usado de qualquer local no aplicativo. Para saber mais sobre como definir o escopo de seus recursos, consulte [Recursos XAML](../../../../docs/framework/wpf/advanced/xaml-resources.md).  
  
2.  **Criar um estilo e definir valores básicos da propriedade com ele:** adicione a seguinte marcação ao bloco `Application.Resources`. Essa marcação cria um <xref:System.Windows.Style> que se aplica a todos os botões no aplicativo, definindo o <xref:System.Windows.FrameworkElement.Width%2A> dos botões como 90 e <xref:System.Windows.FrameworkElement.Margin%2A> para 10:  
  
    ```xaml  
    <Application.Resources>  
      <Style TargetType="Button">
        <Setter Property="Width" Value="90" />
        <Setter Property="Margin" Value="10" />
      </Style>  
    </Application.Resources>  
    ```  
  
     O <xref:System.Windows.Style.TargetType%2A> propriedade especifica que o estilo se aplica a todos os objetos do tipo <xref:System.Windows.Controls.Button>. Cada <xref:System.Windows.Setter> define um valor de propriedade diferente para o <xref:System.Windows.Style>. Portanto, neste ponto, cada botão no aplicativo tem uma largura de 90 e uma margem de 10.  Se você pressionar F5 para executar o aplicativo, você verá a seguinte janela.  
  
     ![Botões com uma largura de 90 e uma margem de 10](../../../../docs/framework/wpf/controls/media/custom-button-animatedbutton-2.gif "custom_button_AnimatedButton_2")  
  
     Há muito mais que você pode fazer com estilos, incluindo uma variedade de maneiras de ajustar quais objetos são direcionados, especificando valores da propriedade complexos e até mesmo usar estilos como entrada para outros estilos. Para obter mais informações, consulte [Estilo e modelagem](../../../../docs/framework/wpf/controls/styling-and-templating.md).  
  
3.  **Definir um valor da propriedade de estilo para um recurso:** os recursos proporcionam uma maneira simples de reutilizar objetos e valores comumente definidos. É especialmente útil definir valores complexos usando recursos para tornar seu código mais modular. Adicione a seguinte marcação realçada ao app.xaml.  
  
    ```xaml  
    <Application.Resources>  
      <LinearGradientBrush x:Key="GrayBlueGradientBrush" StartPoint="0,0" EndPoint="1,1">
        <GradientStop Color="DarkGray" Offset="0" />
        <GradientStop Color="#CCCCFF" Offset="0.5" />
        <GradientStop Color="DarkGray" Offset="1" />
      </LinearGradientBrush>  
      <Style TargetType="{x:Type Button}">  
        <Setter Property="Background" Value="{StaticResource GrayBlueGradientBrush}" />  
        <Setter Property="Width" Value="80" />  
        <Setter Property="Margin" Value="10" />  
      </Style>  
    </Application.Resources>  
    ```  
  
     Logo após o bloco `Application.Resources`, você criou um recurso chamado "GrayBlueGradientBrush". Este recurso define um gradiente horizontal. Esse recurso pode ser usado como um valor de propriedade de qualquer lugar no aplicativo, incluindo dentro de configurador de estilo do botão para o <xref:System.Windows.Controls.Control.Background%2A> propriedade. Agora, todos os botões têm um <xref:System.Windows.Controls.Control.Background%2A> valor da propriedade desse gradiente.  
  
     Pressione F5 para executar o aplicativo. Ele deverá ter a seguinte aparência.  
  
     ![Botões com uma tela de fundo gradiente](../../../../docs/framework/wpf/controls/media/custom-button-animatedbutton-3.gif "custom_button_AnimatedButton_3")  
  
## <a name="create-a-template-that-defines-the-look-of-the-button"></a>Criar um modelo que define a aparência do botão  
 Nesta seção, você cria um modelo que personaliza a aparência (apresentação) do botão. A apresentação do botão é composta de vários objetos, incluindo retângulos e outros componentes, para dar uma aparência exclusiva ao botão.  
  
 Até agora, o controle de como os botões se parecem no aplicativo esteve restrito à alteração das propriedades do botão. E se você quiser fazer alterações mais radicais à aparência do botão? Os modelos proporcionam um controle poderoso sobre a apresentação de um objeto. Como os modelos podem ser usados em estilos, você pode aplicar um modelo a todos os objetos aos quais o estilo se aplica (neste passo a passo, o botão).  
  
#### <a name="to-use-the-template-to-define-the-look-of-the-button"></a>Para usar o modelo para definir a aparência do botão  
  
1.  **Configurar o modelo:** porque controles como <xref:System.Windows.Controls.Button> tem um <xref:System.Windows.Controls.Control.Template%2A> propriedade, você pode definir o valor da propriedade modelo assim como os valores de propriedade que definimos em um <xref:System.Windows.Style> usando um <xref:System.Windows.Setter>. Adicione a seguinte marcação realçada ao seu estilo de botão.  
  
    ```xaml
    <Application.Resources>  
      <LinearGradientBrush x:Key="GrayBlueGradientBrush"   
        StartPoint="0,0" EndPoint="1,1">  
        <GradientStop Color="DarkGray" Offset="0" />  
        <GradientStop Color="#CCCCFF" Offset="0.5" />  
        <GradientStop Color="DarkGray" Offset="1" />  
      </LinearGradientBrush>  
      <Style TargetType="{x:Type Button}">  
        <Setter Property="Background" Value="{StaticResource GrayBlueGradientBrush}" />  
        <Setter Property="Width" Value="80" />  
        <Setter Property="Margin" Value="10" />  
        <Setter Property="Template">
          <Setter.Value>
            <!-- The button template is defined here. -->
          </Setter.Value>
        </Setter>  
      </Style>  
    </Application.Resources>  
    ```  
  
2.  **Alterar apresentação do botão:** neste ponto, você precisa definir o modelo. Adicione a seguinte marcação realçada. Essa marcação especifica dois <xref:System.Windows.Shapes.Rectangle> elementos com bordas arredondadas, seguido por um <xref:System.Windows.Controls.DockPanel>. O <xref:System.Windows.Controls.DockPanel> é usado para hospedar o <xref:System.Windows.Controls.ContentPresenter> do botão. Um <xref:System.Windows.Controls.ContentPresenter> exibe o conteúdo do botão. Neste passo a passo, o conteúdo é texto ("Botão 1", "Botão 2" e "Botão 3"). Todos os componentes de modelo (os retângulos e o <xref:System.Windows.Controls.DockPanel>) são dispostos dentro de um <xref:System.Windows.Controls.Grid>.  
  
    ```xaml  
    <Setter.Value>  
      <ControlTemplate TargetType="Button">
        <Grid Width="{TemplateBinding Width}" Height="{TemplateBinding Height}" ClipToBounds="True">
          <!-- Outer Rectangle with rounded corners. -->
          <Rectangle x:Name="outerRectangle" HorizontalAlignment="Stretch" VerticalAlignment="Stretch" Stroke="{TemplateBinding Background}" RadiusX="20" RadiusY="20" StrokeThickness="5" Fill="Transparent" />
          <!-- Inner Rectangle with rounded corners. -->
          <Rectangle x:Name="innerRectangle" HorizontalAlignment="Stretch" VerticalAlignment="Stretch" Stroke="Transparent" StrokeThickness="20" Fill="{TemplateBinding Background}" RadiusX="20" RadiusY="20" />
          <!-- Present Content (text) of the button. -->
          <DockPanel Name="myContentPresenterDockPanel">
            <ContentPresenter x:Name="myContentPresenter" Margin="20" Content="{TemplateBinding  Content}" TextBlock.Foreground="Black" />
          </DockPanel>
        </Grid>
      </ControlTemplate>  
    </Setter.Value>  
    ```  
  
     Pressione F5 para executar o aplicativo. Ele deverá ter a seguinte aparência.  
  
     ![](../../../../docs/framework/wpf/controls/media/custom-button-animatedbutton-4.gif "custom_button_AnimatedButton_4")  
  
3.  **Adicionar um efeito de vidro ao modelo:** em seguida, você adicionará o vidro. Primeiro, você cria alguns recursos que produzem um efeito de gradiente de vidro. Adicione esses recursos de gradiente em qualquer local no bloco `Application.Resources`:  
  
    ```xaml  
    <Application.Resources>  
      <GradientStopCollection x:Key="MyGlassGradientStopsResource">     <GradientStop Color="WhiteSmoke" Offset="0.2" />     <GradientStop Color="Transparent" Offset="0.4" />     <GradientStop Color="WhiteSmoke" Offset="0.5" />     <GradientStop Color="Transparent" Offset="0.75" />     <GradientStop Color="WhiteSmoke" Offset="0.9" />     <GradientStop Color="Transparent" Offset="1" />   </GradientStopCollection>   <LinearGradientBrush x:Key="MyGlassBrushResource"     StartPoint="0,0" EndPoint="1,1" Opacity="0.75"     GradientStops="{StaticResource MyGlassGradientStopsResource}" />  
    <!-- Styles and other resources below here. -->  
    ```  
  
     Esses recursos são usados como o <xref:System.Windows.Shapes.Shape.Fill%2A> para um retângulo que podemos inserir a <xref:System.Windows.Controls.Grid> do modelo de botão. Adicione a seguinte marcação realçada ao modelo.  
  
    ```  
    <Setter.Value>  
      <ControlTemplate TargetType="{x:Type Button}">  
        <Grid Width="{TemplateBinding Width}" Height="{TemplateBinding Height}"  
    ClipToBounds="True">  
  
        <!-- Outer Rectangle with rounded corners. -->  
        <Rectangle x:Name="outerRectangle" HorizontalAlignment="Stretch"   
          VerticalAlignment="Stretch" Stroke="{TemplateBinding Background}"   
          RadiusX="20" RadiusY="20" StrokeThickness="5" Fill="Transparent" />  
  
        <!-- Inner Rectangle with rounded corners. -->  
        <Rectangle x:Name="innerRectangle" HorizontalAlignment="Stretch"   
          VerticalAlignment="Stretch" Stroke="Transparent" StrokeThickness="20"   
          Fill="{TemplateBinding Background}" RadiusX="20" RadiusY="20" />  
  
        <!-- Glass Rectangle -->     <Rectangle x:Name="glassCube" HorizontalAlignment="Stretch"       VerticalAlignment="Stretch"       StrokeThickness="2" RadiusX="10" RadiusY="10" Opacity="0"       Fill="{StaticResource MyGlassBrushResource}"       RenderTransformOrigin="0.5,0.5">       <Rectangle.Stroke>         <LinearGradientBrush StartPoint="0.5,0" EndPoint="0.5,1">           <LinearGradientBrush.GradientStops>             <GradientStop Offset="0.0" Color="LightBlue" />             <GradientStop Offset="1.0" Color="Gray" />           </LinearGradientBrush.GradientStops>         </LinearGradientBrush>       </Rectangle.Stroke>       <!-- These transforms have no effect as they are declared here.             The reason the transforms are included is to be targets             for animation (see later). -->       <Rectangle.RenderTransform>         <TransformGroup>           <ScaleTransform />           <RotateTransform />         </TransformGroup>       </Rectangle.RenderTransform>       <!-- A BevelBitmapEffect is applied to give the button a             "Beveled" look. -->       <Rectangle.BitmapEffect>         <BevelBitmapEffect />       </Rectangle.BitmapEffect>     </Rectangle>  
  
        <!-- Present Text of the button. -->  
        <DockPanel Name="myContentPresenterDockPanel">  
          <ContentPresenter x:Name="myContentPresenter" Margin="20"   
            Content="{TemplateBinding  Content}" TextBlock.Foreground="Black" />  
        </DockPanel>  
      </Grid>  
    </ControlTemplate>  
    </Setter.Value>  
    ```  
  
     Observe que o <xref:System.Windows.UIElement.Opacity%2A> do retângulo com o `x:Name` propriedade de "glassCube" é 0, portanto, quando você executar o exemplo, você não vir o retângulo de vidro sobreposto na parte superior. Isso é assim porque depois adicionaremos gatilhos ao modelo para quando o usuário interagir com o botão. No entanto, você pode ver o botão aparência agora alterando o <xref:System.Windows.UIElement.Opacity%2A> valor para 1 e executando o aplicativo. Veja a figura a seguir. Antes de prosseguir para a próxima etapa, altere o <xref:System.Windows.UIElement.Opacity%2A> volta para 0.  
  
     ![Botões personalizados criados com XAML](../../../../docs/framework/wpf/controls/media/custom-button-animatedbutton-5.gif "custom_button_AnimatedButton_5")  
  
## <a name="create-button-interactivity"></a>Criar interatividade de botão  
 Nesta seção, você criará gatilhos de propriedade e gatilhos de evento para alterar os valores da propriedade e executar animações em resposta às ações do usuário, como mover o ponteiro do mouse sobre o botão e clicar.  
  
 Uma maneira fácil de adicionar interatividade (passar o mouse, soltar o mouse, clicar e assim por diante) é definir gatilhos dentro de seu modelo ou estilo. Para criar um <xref:System.Windows.Trigger>, você define uma propriedade "condição" como: O botão <xref:System.Windows.UIElement.IsMouseOver%2A> o valor da propriedade é igual a `true`. Em seguida, você define setters (ações) que ocorrem quando a condição do gatilho for verdadeira.  
  
#### <a name="to-create-button-interactivity"></a>Para criar interatividade de botão  
  
1.  **Adicionar modelos de gatilho:** adicione a marcação realçada ao seu modelo.  
  
    ```  
    <Setter.Value>  
      <ControlTemplate TargetType="{x:Type Button}">  
        <Grid Width="{TemplateBinding Width}"   
          Height="{TemplateBinding Height}" ClipToBounds="True">  
  
          <!-- Outer Rectangle with rounded corners. -->  
          <Rectangle x:Name="outerRectangle" HorizontalAlignment="Stretch"   
          VerticalAlignment="Stretch" Stroke="{TemplateBinding Background}"   
          RadiusX="20" RadiusY="20" StrokeThickness="5" Fill="Transparent" />  
  
          <!-- Inner Rectangle with rounded corners. -->  
          <Rectangle x:Name="innerRectangle" HorizontalAlignment="Stretch"   
            VerticalAlignment="Stretch" Stroke="Transparent"   
            StrokeThickness="20"   
            Fill="{TemplateBinding Background}" RadiusX="20" RadiusY="20"   
          />  
  
          <!-- Glass Rectangle -->  
          <Rectangle x:Name="glassCube" HorizontalAlignment="Stretch"  
            VerticalAlignment="Stretch"  
            StrokeThickness="2" RadiusX="10" RadiusY="10" Opacity="0"  
            Fill="{StaticResource MyGlassBrushResource}"  
            RenderTransformOrigin="0.5,0.5">  
            <Rectangle.Stroke>  
              <LinearGradientBrush StartPoint="0.5,0" EndPoint="0.5,1">  
                <LinearGradientBrush.GradientStops>  
                  <GradientStop Offset="0.0" Color="LightBlue" />  
                  <GradientStop Offset="1.0" Color="Gray" />  
                </LinearGradientBrush.GradientStops>  
              </LinearGradientBrush>  
            </Rectangle.Stroke>  
  
            <!-- These transforms have no effect as they   
                 are declared here.   
                 The reason the transforms are included is to be targets   
                 for animation (see later). -->  
            <Rectangle.RenderTransform>  
              <TransformGroup>  
                <ScaleTransform />  
                <RotateTransform />  
              </TransformGroup>  
            </Rectangle.RenderTransform>  
  
              <!-- A BevelBitmapEffect is applied to give the button a   
                   "Beveled" look. -->  
            <Rectangle.BitmapEffect>  
              <BevelBitmapEffect />  
            </Rectangle.BitmapEffect>  
          </Rectangle>  
  
          <!-- Present Text of the button. -->  
          <DockPanel Name="myContentPresenterDockPanel">  
            <ContentPresenter x:Name="myContentPresenter" Margin="20"   
              Content="{TemplateBinding  Content}" TextBlock.Foreground="Black" />  
          </DockPanel>  
        </Grid>  
  
        <ControlTemplate.Triggers>       <!-- Set action triggers for the buttons and define            what the button does in response to those triggers. -->     </ControlTemplate.Triggers>  
      </ControlTemplate>  
    </Setter.Value>  
    ```  
  
2.  **Adicionar gatilhos de propriedade:** adicionar a marcação realçada ao bloco `ControlTemplate.Triggers`:  
  
    ```  
    <ControlTemplate.Triggers>  
  
      <!-- Set properties when mouse pointer is over the button. -->   <Trigger Property="IsMouseOver" Value="True">     <!-- Below are three property settings that occur when the           condition is met (user mouses over button).  -->     <!-- Change the color of the outer rectangle when user           mouses over it. -->     <Setter Property ="Rectangle.Stroke" TargetName="outerRectangle"       Value="{DynamicResource {x:Static SystemColors.HighlightBrushKey}}" />     <!-- Sets the glass opacity to 1, therefore, the           glass "appears" when user mouses over it. -->     <Setter Property="Rectangle.Opacity" Value="1" TargetName="glassCube" />     <!-- Makes the text slightly blurry as though you           were looking at it through blurry glass. -->     <Setter Property="ContentPresenter.BitmapEffect"        TargetName="myContentPresenter">       <Setter.Value>         <BlurBitmapEffect Radius="1" />       </Setter.Value>     </Setter>   </Trigger>  
  
    <ControlTemplate.Triggers/>  
    ```  
  
     Pressione F5 para executar o aplicativo e veja o efeito ao passar o ponteiro do mouse sobre os botões.  
  
3.  **Adicionar um gatilho de foco:** em seguida, adicionaremos alguns setters semelhantes para manipular o caso em que o botão tiver o foco (por exemplo, depois que o usuário clica nele).  
  
    ```  
    <ControlTemplate.Triggers>  
  
      <!-- Set properties when mouse pointer is over the button. -->  
      <Trigger Property="IsMouseOver" Value="True">  
  
        <!-- Below are three property settings that occur when the   
             condition is met (user mouses over button).  -->  
        <!-- Change the color of the outer rectangle when user          mouses over it. -->  
        <Setter Property ="Rectangle.Stroke" TargetName="outerRectangle"  
          Value="{DynamicResource {x:Static SystemColors.HighlightBrushKey}}" />  
  
        <!-- Sets the glass opacity to 1, therefore, the          glass "appears" when user mouses over it. -->  
        <Setter Property="Rectangle.Opacity" Value="1"       TargetName="glassCube" />  
  
        <!-- Makes the text slightly blurry as though you were          looking at it through blurry glass. -->  
        <Setter Property="ContentPresenter.BitmapEffect"       TargetName="myContentPresenter">  
          <Setter.Value>  
            <BlurBitmapEffect Radius="1" />  
          </Setter.Value>  
        </Setter>  
      </Trigger>  
      <!-- Set properties when button has focus. -->   <Trigger Property="IsFocused" Value="true">     <Setter Property="Rectangle.Opacity" Value="1"       TargetName="glassCube" />     <Setter Property="Rectangle.Stroke" TargetName="outerRectangle"       Value="{DynamicResource {x:Static SystemColors.HighlightBrushKey}}" />     <Setter Property="Rectangle.Opacity" Value="1" TargetName="glassCube" />   </Trigger>  
  
    </ControlTemplate.Triggers>  
    ```  
  
     Pressione F5 para executar o aplicativo e clique em um dos botões. Observe que o botão permanece realçado depois que você clica nele, porque ele ainda tem foco. Se você clicar em outro botão, o novo botão obtém o foco e o outro perde o foco.  
  
4.  **Adicionar animações para** <xref:System.Windows.UIElement.MouseEnter> **e** <xref:System.Windows.UIElement.MouseLeave> **:** lado adicionamos algumas animações para os gatilhos. Adicione a seguinte marcação em qualquer local dentro do bloco `ControlTemplate.Triggers`.  
  
    ```  
    <!-- Animations that start when mouse enters and leaves button. -->  
    <EventTrigger RoutedEvent="Mouse.MouseEnter">  
      <EventTrigger.Actions>  
        <BeginStoryboard Name="mouseEnterBeginStoryboard">  
          <Storyboard>  
          <!-- This animation makes the glass rectangle shrink in the X direction. -->  
            <DoubleAnimation Storyboard.TargetName="glassCube"   
              Storyboard.TargetProperty=  
              "(Rectangle.RenderTransform).(TransformGroup.Children)[0].(ScaleTransform.ScaleX)"  
              By="-0.1" Duration="0:0:0.5" />  
            <!-- This animation makes the glass rectangle shrink in the Y direction. -->  
            <DoubleAnimation  
            Storyboard.TargetName="glassCube"   
              Storyboard.TargetProperty=  
              "(Rectangle.RenderTransform).(TransformGroup.Children)[0].(ScaleTransform.ScaleY)"   
              By="-0.1" Duration="0:0:0.5" />  
          </Storyboard>  
        </BeginStoryboard>  
      </EventTrigger.Actions>  
    </EventTrigger>  
    <EventTrigger RoutedEvent="Mouse.MouseLeave">  
      <EventTrigger.Actions>  
        <!-- Stopping the storyboard sets all animated properties back to default. -->  
        <StopStoryboard BeginStoryboardName="mouseEnterBeginStoryboard" />  
      </EventTrigger.Actions>  
    </EventTrigger>  
    ```  
  
     O retângulo de vidro é reduzido quando o ponteiro do mouse passa sobre o botão e retorna ao tamanho normal quando o ponteiro sai.  
  
     Há duas animações que são acionadas quando o ponteiro passa sobre o botão (<xref:System.Windows.UIElement.MouseEnter> é gerado). Essas animações reduzem o retângulo de vidro ao longo dos eixos X e Y. Observe as propriedades no <xref:System.Windows.Media.Animation.DoubleAnimation> elementos — <xref:System.Windows.Media.Animation.Timeline.Duration%2A> e <xref:System.Windows.Media.Animation.DoubleAnimation.By%2A>. O <xref:System.Windows.Media.Animation.Timeline.Duration%2A> Especifica que a animação ocorre por meio segundo, e <xref:System.Windows.Media.Animation.DoubleAnimation.By%2A> Especifica que o vidro se reduz por 10%.  
  
     O segundo gatilho de evento (<xref:System.Windows.UIElement.MouseLeave>) simplesmente para o primeiro. Quando você interrompe um <xref:System.Windows.Media.Animation.Storyboard>, retornarem todas as propriedades de animação para seus valores padrão. Portanto, quando o usuário move o ponteiro para fora do botão, o botão volta à forma que estava antes de o ponteiro do mouse ser passado sobre o botão. Para obter mais informações sobre animações, consulte [Visão geral de animação](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md).  
  
5.  **Adicionar uma animação para quando o botão é clicado:** a etapa final é adicionar um gatilho para quando o usuário clica no botão. Adicione a seguinte marcação em qualquer local dentro do bloco `ControlTemplate.Triggers`:  
  
    ```  
    <!-- Animation fires when button is clicked, causing glass to spin.  -->  
    <EventTrigger RoutedEvent="Button.Click">  
      <EventTrigger.Actions>  
        <BeginStoryboard>  
          <Storyboard>  
            <DoubleAnimation Storyboard.TargetName="glassCube"   
              Storyboard.TargetProperty=  
              "(Rectangle.RenderTransform).(TransformGroup.Children)[1].(RotateTransform.Angle)"   
              By="360" Duration="0:0:0.5" />  
          </Storyboard>  
        </BeginStoryboard>  
      </EventTrigger.Actions>  
    </EventTrigger>  
    ```  
  
     Pressione F5 para executar o aplicativo e clique em um dos botões. Quando você clica em um botão, o retângulo de vidro faz um giro.  
  
## <a name="summary"></a>Resumo  
 Neste passo a passo, você realizou os seguintes exercícios:  
  
-   Destino um <xref:System.Windows.Style> para um tipo de objeto (<xref:System.Windows.Controls.Button>).  
  
-   Controlado propriedades básicas dos botões em todo o aplicativo usando o <xref:System.Windows.Style>.  
  
-   Criou recursos como gradientes a serem usados para valores de propriedade de <xref:System.Windows.Style> setters.  
  
-   Personalizou a aparência dos botões em todo o aplicativo, aplicando um modelo aos botões.  
  
-   Personalizou comportamento para os botões em resposta a ações do usuário (como <xref:System.Windows.UIElement.MouseEnter>, <xref:System.Windows.UIElement.MouseLeave>, e <xref:System.Windows.Controls.Primitives.ButtonBase.Click>) que incluiu efeitos de animação.  
  
## <a name="see-also"></a>Consulte também  
 [Criar um botão usando o Microsoft Expression Blend](../../../../docs/framework/wpf/controls/walkthrough-create-a-button-by-using-microsoft-expression-blend.md)  
 [Estilo e modelagem](../../../../docs/framework/wpf/controls/styling-and-templating.md)  
 [Visão geral da animação](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)  
 [Visão geral da pintura com cores sólidas e gradientes](../../../../docs/framework/wpf/graphics-multimedia/painting-with-solid-colors-and-gradients-overview.md)  
 [Visão geral dos efeitos de bitmap](../../../../docs/framework/wpf/graphics-multimedia/bitmap-effects-overview.md)
