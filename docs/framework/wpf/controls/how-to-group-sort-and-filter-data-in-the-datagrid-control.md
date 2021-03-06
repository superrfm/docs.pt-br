---
title: Como agrupar, classificar e filtrar dados no controle DataGrid
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-wpf
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- csharp
- vb
helpviewer_keywords:
- DataGrid [WPF], sort
- DataGrid [WPF], group
- DataGrid [WPF], filter
ms.assetid: 03345e85-89e3-4aec-9ed0-3b80759df770
caps.latest.revision: "8"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: e648b5a4a45c3583d496ac0ea6036d268d6d33a6
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/22/2017
---
# <a name="how-to-group-sort-and-filter-data-in-the-datagrid-control"></a>Como agrupar, classificar e filtrar dados no controle DataGrid
Geralmente é útil exibir dados em um <xref:System.Windows.Controls.DataGrid> de diferentes maneiras por agrupamento, classificação e filtragem dos dados. Para agrupar, classificar e filtrar os dados em um <xref:System.Windows.Controls.DataGrid>, você associa um <xref:System.Windows.Data.CollectionView> que dá suporte a essas funções. Em seguida, você pode trabalhar com os dados de <xref:System.Windows.Data.CollectionView> sem afetar os dados de origem subjacentes. As alterações no modo de exibição de coleção são refletidas no <xref:System.Windows.Controls.DataGrid> interface do usuário (IU).  
  
 O <xref:System.Windows.Data.CollectionView> classe fornece agrupando e classificando funcionalidade para uma fonte de dados que implementa o <xref:System.Collections.IEnumerable> interface. O <xref:System.Windows.Data.CollectionViewSource> classe permite que você defina as propriedades de um <xref:System.Windows.Data.CollectionView> do XAML.  
  
 Neste exemplo, uma coleção de `Task` objetos está associado a um <xref:System.Windows.Data.CollectionViewSource>. O <xref:System.Windows.Data.CollectionViewSource> é usado como o <xref:System.Windows.Controls.ItemsControl.ItemsSource%2A> para o <xref:System.Windows.Controls.DataGrid>. Agrupamento, classificação e filtragem são executadas no <xref:System.Windows.Data.CollectionViewSource> e são exibidos no <xref:System.Windows.Controls.DataGrid> interface do usuário.  
  
 ![Dados agrupados em uma grade de dados](../../../../docs/framework/wpf/controls/media/wpf-datagridgroups.png "WPF_DataGridGroups")  
Dados Agrupados em um DataGrid  
  
## <a name="using-a-collectionviewsource-as-an-itemssource"></a>Usando um CollectionViewSource como ItemsSource  
 Para o grupo, classificar e filtrar dados em um <xref:System.Windows.Controls.DataGrid> controle, você associa o <xref:System.Windows.Controls.DataGrid> para um <xref:System.Windows.Data.CollectionView> que dá suporte a essas funções. Neste exemplo, o <xref:System.Windows.Controls.DataGrid> está associado a um <xref:System.Windows.Data.CollectionViewSource> que fornece essas funções para um <xref:System.Collections.Generic.List%601> de `Task` objetos.  
  
#### <a name="to-bind-a-datagrid-to-a-collectionviewsource"></a>Para associar um DataGrid a um CollectionViewSource  
  
1.  Criar uma coleção de dados que implementa o <xref:System.Collections.IEnumerable> interface.  
  
     Se você usar <xref:System.Collections.Generic.List%601> para criar sua coleção, você deve criar uma nova classe que herda de <xref:System.Collections.Generic.List%601> em vez de instanciar uma instância de <xref:System.Collections.Generic.List%601>. Isso permite associar dados à coleção em XAML.  
  
    > [!NOTE]
    >  Os objetos na coleção devem implementar a <xref:System.ComponentModel.INotifyPropertyChanged> interface alterado e o <xref:System.ComponentModel.IEditableObject> interface para que o <xref:System.Windows.Controls.DataGrid> responder corretamente a alterações de propriedade e edições. Para obter mais informações, consulte [Implementar notificação de alteração da propriedade](../../../../docs/framework/wpf/data/how-to-implement-property-change-notification.md).  
  
     [!code-csharp[DataGrid_GroupSortFilter#101](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DataGrid_GroupSortFilter/CS/MainWindow.xaml.cs#101)]
     [!code-vb[DataGrid_GroupSortFilter#101](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DataGrid_GroupSortFilter/VB/MainWindow.xaml.vb#101)]  
  
2.  No XAML, crie uma instância da classe de coleção e defina a [Diretiva x:Key](../../../../docs/framework/xaml-services/x-key-directive.md).  
  
3.  No XAML, crie uma instância do <xref:System.Windows.Data.CollectionViewSource> classe, defina o [diretiva X:Key](../../../../docs/framework/xaml-services/x-key-directive.md)e defina a instância de sua classe de coleção como o <xref:System.Windows.Data.CollectionViewSource.Source%2A>.  
  
     [!code-xaml[DataGrid_GroupSortFilter#201](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DataGrid_GroupSortFilter/CS/WindowSnips1.xaml#201)]  
  
4.  Criar uma instância do <xref:System.Windows.Controls.DataGrid> de classe e defina o <xref:System.Windows.Controls.ItemsControl.ItemsSource%2A> propriedade para o <xref:System.Windows.Data.CollectionViewSource>.  
  
     [!code-xaml[DataGrid_GroupSortFilter#002](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DataGrid_GroupSortFilter/CS/MainWindow.xaml#002)]  
  
5.  Para acessar o <xref:System.Windows.Data.CollectionViewSource> do seu código, use o <xref:System.Windows.Data.CollectionViewSource.GetDefaultView%2A> método para obter uma referência para o <xref:System.Windows.Data.CollectionViewSource>.  
  
     [!code-csharp[DataGrid_GroupSortFilter#102](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DataGrid_GroupSortFilter/CS/MainWindow.xaml.cs#102)]
     [!code-vb[DataGrid_GroupSortFilter#102](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DataGrid_GroupSortFilter/VB/MainWindow.xaml.vb#102)]  
  
## <a name="grouping-items-in-a-datagrid"></a>Agrupando itens em um DataGrid  
 Para especificar como os itens são agrupados em um <xref:System.Windows.Controls.DataGrid>, você usa o <xref:System.Windows.Data.PropertyGroupDescription> tipo para agrupar os itens na exibição da fonte.  
  
#### <a name="to-group-items-in-a-datagrid-using-xaml"></a>Para agrupar itens em um DataGrid usando XAML  
  
1.  Criar um <xref:System.Windows.Data.PropertyGroupDescription> que especifica a propriedade para agrupar por. Você pode especificar a propriedade no XAML ou no código.  
  
    1.  Em XAML, definir o <xref:System.Windows.Data.PropertyGroupDescription.PropertyName%2A> para o nome da propriedade para agrupar por.  
  
    2.  No código, passe o nome da propriedade segundo a qual o agrupamento será feito ao construtor.  
  
2.  Adicionar o <xref:System.Windows.Data.PropertyGroupDescription> para o <xref:System.Windows.Data.CollectionViewSource.GroupDescriptions%2A?displayProperty=nameWithType> coleção.  
  
3.  Adicione instâncias adicionais do <xref:System.Windows.Data.PropertyGroupDescription> para o <xref:System.Windows.Data.CollectionViewSource.GroupDescriptions%2A> coleção para adicionar mais níveis de agrupamento.  
  
     [!code-xaml[DataGrid_GroupSortFilter#012](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DataGrid_GroupSortFilter/CS/MainWindow.xaml#012)]  
  
     [!code-csharp[DataGrid_GroupSortFilter#112](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DataGrid_GroupSortFilter/CS/MainWindow.xaml.cs#112)]
     [!code-vb[DataGrid_GroupSortFilter#112](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DataGrid_GroupSortFilter/VB/MainWindow.xaml.vb#112)]  
  
4.  Para remover um grupo, remova o <xref:System.Windows.Data.PropertyGroupDescription> do <xref:System.Windows.Data.CollectionViewSource.GroupDescriptions%2A> coleção.  
  
5.  Para remover todos os grupos, chame o <xref:System.Collections.ObjectModel.Collection%601.Clear%2A> método o <xref:System.Windows.Data.CollectionViewSource.GroupDescriptions%2A> coleção.  
  
     [!code-csharp[DataGrid_GroupSortFilter#114](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DataGrid_GroupSortFilter/CS/MainWindow.xaml.cs#114)]
     [!code-vb[DataGrid_GroupSortFilter#114](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DataGrid_GroupSortFilter/VB/MainWindow.xaml.vb#114)]  
  
 Quando os itens são agrupados no <xref:System.Windows.Controls.DataGrid>, você pode definir um <xref:System.Windows.Controls.GroupStyle> que especifica a aparência de cada grupo. Aplicar o <xref:System.Windows.Controls.GroupStyle> ao ser adicionado a <xref:System.Windows.Controls.ItemsControl.GroupStyle%2A> coleção da grade de dados. Se tiver vários níveis de agrupamento, você poderá aplicar estilos diferentes a cada nível de grupo. Os estilos são aplicados na ordem em que são definidos. Por exemplo, se você definir dois estilos, o primeiro será aplicado a grupos de linhas de nível superior. O segundo estilo será aplicado a todos os grupos de linhas no segundo nível e abaixo. O <xref:System.Windows.FrameworkElement.DataContext%2A> do <xref:System.Windows.Controls.GroupStyle> é o <xref:System.Windows.Data.CollectionViewGroup> que representa o grupo.  
  
#### <a name="to-change-the-appearance-of-row-group-headers"></a>Para alterar a aparência dos cabeçalhos de grupos de linhas  
  
1.  Criar um <xref:System.Windows.Controls.GroupStyle> que define a aparência do grupo de linhas.  
  
2.  Coloque o <xref:System.Windows.Controls.GroupStyle> dentro de `<DataGrid.GroupStyle>` marcas.  
  
     [!code-xaml[DataGrid_GroupSortFilter#003](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DataGrid_GroupSortFilter/CS/MainWindow.xaml#003)]  
  
## <a name="sorting-items-in-a-datagrid"></a>Classificando itens em um DataGrid  
 Para especificar como os itens são classificados em uma <xref:System.Windows.Controls.DataGrid>, você usa o <xref:System.ComponentModel.SortDescription> tipo para classificar os itens na exibição da fonte.  
  
#### <a name="to-sort-items-in-a-datagrid"></a>Para classificar itens em um DataGrid  
  
1.  Criar um <xref:System.ComponentModel.SortDescription> que especifica a propriedade classificar por. Você pode especificar a propriedade no XAML ou no código.  
  
    1.  Em XAML, definir o <xref:System.ComponentModel.SortDescription.PropertyName%2A> para o nome da propriedade de classificação.  
  
    2.  No código, passe o nome da propriedade de classificação e o <xref:System.ComponentModel.ListSortDirection> para o construtor.  
  
2.  Adicionar o <xref:System.ComponentModel.SortDescription> para o <xref:System.Windows.Data.CollectionViewSource.SortDescriptions%2A?displayProperty=nameWithType> coleção.  
  
3.  Adicione instâncias adicionais do <xref:System.ComponentModel.SortDescription> para o <xref:System.Windows.Data.CollectionViewSource.SortDescriptions%2A> coleção para classificar por propriedades adicionais.  
  
     [!code-xaml[DataGrid_GroupSortFilter#011](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DataGrid_GroupSortFilter/CS/MainWindow.xaml#011)]  
  
     [!code-csharp[DataGrid_GroupSortFilter#211](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DataGrid_GroupSortFilter/CS/WindowSnips1.xaml.cs#211)]
     [!code-vb[DataGrid_GroupSortFilter#211](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DataGrid_GroupSortFilter/VB/MainWindow.xaml.vb#211)]  
  
## <a name="filtering-items-in-a-datagrid"></a>Filtrando itens em um DataGrid  
 Para filtrar itens em uma <xref:System.Windows.Controls.DataGrid> usando um <xref:System.Windows.Data.CollectionViewSource>, forneça a lógica de filtragem no manipulador para o <xref:System.Windows.Data.CollectionViewSource.Filter?displayProperty=nameWithType> evento.  
  
#### <a name="to-filter-items-in-a-datagrid"></a>Para filtrar itens em um DataGrid  
  
1.  Adicionar um manipulador para o <xref:System.Windows.Data.CollectionViewSource.Filter?displayProperty=nameWithType> evento.  
  
2.  No <xref:System.Windows.Data.CollectionViewSource.Filter> manipulador de eventos, definir a lógica de filtragem.  
  
     O filtro será aplicado sempre que a exibição for atualizada.  
  
     [!code-xaml[DataGrid_GroupSortFilter#013](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DataGrid_GroupSortFilter/CS/MainWindow.xaml#013)]  
  
     [!code-csharp[DataGrid_GroupSortFilter#113](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DataGrid_GroupSortFilter/CS/MainWindow.xaml.cs#113)]
     [!code-vb[DataGrid_GroupSortFilter#113](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DataGrid_GroupSortFilter/VB/MainWindow.xaml.vb#113)]  
  
 Como alternativa, você pode filtrar itens em uma <xref:System.Windows.Controls.DataGrid> criando um método que fornece a lógica de filtragem e configuração de <xref:System.Windows.Data.CollectionView.Filter%2A?displayProperty=nameWithType> propriedade para aplicar o filtro. Para ver um exemplo desse método, consulte [Filtrar dados em uma exibição](../../../../docs/framework/wpf/data/how-to-filter-data-in-a-view.md).  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir demonstra o agrupamento, classificação e filtragem `Task` dados em um <xref:System.Windows.Data.CollectionViewSource> e exibindo agrupados, classificados e filtrados `Task` dados em um <xref:System.Windows.Controls.DataGrid>. O <xref:System.Windows.Data.CollectionViewSource> é usado como o <xref:System.Windows.Controls.ItemsControl.ItemsSource%2A> para o <xref:System.Windows.Controls.DataGrid>. Agrupamento, classificação e filtragem são executadas no <xref:System.Windows.Data.CollectionViewSource> e são exibidos no <xref:System.Windows.Controls.DataGrid> interface do usuário.  
  
 Para testar este exemplo, você precisará ajustar o nome de DGGroupSortFilterExample para corresponder ao nome do seu projeto. Se você estiver usando o Visual Basic, você precisará alterar o nome da classe para <xref:System.Windows.Window> à seguinte.  
  
 `<Window x:Class="MainWindow"`  
  
 [!code-xaml[DataGrid_GroupSortFilter#000](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DataGrid_GroupSortFilter/CS/MainWindow.xaml#000)]  
  
 [!code-csharp[DataGrid_GroupSortFilter#100](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DataGrid_GroupSortFilter/CS/MainWindow.xaml.cs#100)]
 [!code-vb[DataGrid_GroupSortFilter#100](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DataGrid_GroupSortFilter/VB/MainWindow.xaml.vb#100)]  
  
## <a name="compiling-the-code"></a>Compilando o código  
  
-  
  
## <a name="robust-programming"></a>Programação robusta  
  
## <a name="net-framework-security"></a>Segurança do .NET Framework  
  
## <a name="see-also"></a>Consulte também  
 [Visão geral da vinculação de dados](../../../../docs/framework/wpf/data/data-binding-overview.md)  
 [Criar e associar a um ObservableCollection](../../../../docs/framework/wpf/data/how-to-create-and-bind-to-an-observablecollection.md)  
 [Filtrar dados em uma exibição](../../../../docs/framework/wpf/data/how-to-filter-data-in-a-view.md)  
 [Classificar dados em uma exibição](../../../../docs/framework/wpf/data/how-to-sort-data-in-a-view.md)  
 [Classificar e agrupar dados usando uma exibição em XAML](../../../../docs/framework/wpf/data/how-to-sort-and-group-data-using-a-view-in-xaml.md)
