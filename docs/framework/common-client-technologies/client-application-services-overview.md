---
title: "Visão geral dos serviços de aplicativo cliente"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- client application services, classes
- client application services, about client application services
ms.assetid: f0a2da13-e282-4fd7-88a1-f9102c9aeab1
caps.latest.revision: "25"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 55b4ab154f9f3a9b17274697c30ca826218322ab
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/22/2017
---
# <a name="client-application-services-overview"></a>Visão geral dos serviços de aplicativo cliente
Os serviços de aplicativo cliente fornecem acesso simplificado ao logon, às funções e aos serviços de perfil do [!INCLUDE[ajax_current_short](../../../includes/ajax-current-short-md.md)] por meio dos aplicativos Windows Forms e WPF (Windows Presentation Foundation). Os serviços de aplicativo [!INCLUDE[ajax_current_short](../../../includes/ajax-current-short-md.md)] estão incluídos nas Extensões AJAX do Microsoft ASP.NET 2.0, que estão incluídas no [!INCLUDE[vs_orcas_long](../../../includes/vs-orcas-long-md.md)] e no [!INCLUDE[net_v35_long](../../../includes/net-v35-long-md.md)]. Esses serviços permitem que vários aplicativos Web e baseados no Windows compartilhem informações do usuário e a funcionalidade de gerenciamento de usuários de um único servidor.  
  
 Os serviços de aplicativos cliente incluem provedores de serviço de cliente que se conectam ao modelo de extensibilidade de serviços Web para habilitar os seguintes recursos para aplicativos baseados no Windows:  
  
-   Configuração de cliente simples. Você pode habilitar e configurar o logon, funções e serviços de perfil usando o designer de projeto [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] ou especificando provedores de serviço de cliente no arquivo App.config do projeto. Para obter mais informações, consulte [Como configurar serviços de aplicativo cliente](../../../docs/framework/common-client-technologies/how-to-configure-client-application-services.md).  
  
-   Programação simples. Depois de ter habilitado e configurado os serviços de aplicativos cliente, você pode acessar os provedores de serviços indiretamente por meio de associações [!INCLUDE[dnprdnlong](../../../includes/dnprdnlong-md.md)], funções e classes de configurações do aplicativo. Você também pode acessar diretamente as classes [!INCLUDE[net_v35_long](../../../includes/net-v35-long-md.md)] que implementam os serviços de aplicativos cliente. No entanto, na maioria dos casos, o acesso direto é desnecessário. Para obter mais informações sobre as classes de serviços de aplicativos cliente, consulte a seção “Classes de serviços de aplicativos cliente” deste tópico.  
  
-   Suporte offline. Aplicativos baseados no Windows geralmente têm que operar em ambientes conectados ocasionalmente. Quando seu aplicativo estiver online, os provedores de serviço cliente armazenarão em cache os valores recuperados do servidor para uso quando o aplicativo estiver offline.  
  
-   Integração com o designer de configurações de aplicativo [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)]. Quando você adiciona as configurações ao seu projeto no [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)], pode especificar quais configurações devem ser acessadas por meio do provedor de serviço de configurações do cliente.  
  
 As seções a seguir descrevem esses recursos em mais detalhes. Para obter mais informações sobre os serviços de aplicativos [!INCLUDE[ajax_current_short](../../../includes/ajax-current-short-md.md)], consulte [Visão geral sobre Serviços de Aplicativos ASP.NET](http://msdn.microsoft.com/library/1162e529-0d70-44b2-b3ab-83e60c695013).  
  
## <a name="authentication"></a>Autenticação  
 Você pode usar serviços de aplicativos cliente para validar um usuário por meio de um serviço de autenticação [!INCLUDE[ajax_current_short](../../../includes/ajax-current-short-md.md)] existente. Você pode validar um usuário usando a autenticação do Windows ou de formulários. Autenticação do Windows significa que a identidade do usuário é aquela fornecida pelo sistema operacional quando um usuário faz logon em um computador ou domínio. Normalmente, você usará a autenticação do Windows com um aplicativo implantado em uma intranet corporativa. Autenticação de formulários significa que você deve incluir controles de logon em seu aplicativo e passar as credenciais adquiridas para o provedor de autenticação. Normalmente, você usará a autenticação de formulários com um aplicativo implantado na Internet.  
  
 Para validar um usuário, você chama o método `static` <xref:System.Web.Security.Membership.ValidateUser%2A?displayProperty=nameWithType>. Esse método acessa o provedor de serviço cliente configurado para o seu aplicativo e retorna um valor <xref:System.Boolean> que indica se o usuário é válido. Para obter mais informações, consulte [Como implementar o logon do usuário com os serviços de aplicativo cliente](../../../docs/framework/common-client-technologies/how-to-implement-user-login-with-client-application-services.md).  
  
 Ao usar a autenticação do Windows, você deve passar cadeias de caracteres vazias ou `null` como os parâmetros do método <xref:System.Web.Security.Membership.ValidateUser%2A>. Ao usar a autenticação do Windows, esta chamada de método sempre retornará `true`.  
  
 Com a autenticação de formulários, o método <xref:System.Web.Security.Membership.ValidateUser%2A> retornará um valor que indica se o serviço remoto autenticou o usuário. Se a validação for bem-sucedida, um cookie de autenticação será armazenado no disco rígido local. Esse cookie é usado para confirmar a validação ao acessar os serviços de configurações e funções.  
  
 Ao usar autenticação de formulários, você pode passar um nome de usuário e senha para o método <xref:System.Web.Security.Membership.ValidateUser%2A>. Você também pode passar cadeias de caracteres vazias ou `null` como os parâmetros para usar um provedor de credenciais. Um provedor de credenciais é uma classe que você fornece e especifica em sua configuração de aplicativo. Uma classe de provedor de credenciais deve implementar a interface <xref:System.Web.ClientServices.Providers.IClientFormsAuthenticationCredentialsProvider>, que tem um único método chamado <xref:System.Web.ClientServices.Providers.IClientFormsAuthenticationCredentialsProvider.GetCredentials%2A>. Usar um provedor de credenciais permite que você compartilhe uma única caixa de diálogo de logon entre vários aplicativos. Para obter mais informações, consulte [Como configurar serviços de aplicativo cliente](../../../docs/framework/common-client-technologies/how-to-configure-client-application-services.md).  
  
 Quando você configura seu aplicativo para usar um provedor de credenciais com autenticação de formulários, deve passar cadeias de caracteres vazias ou `null` como os parâmetros do método <xref:System.Web.Security.Membership.ValidateUser%2A>. O provedor de serviços, em seguida, chamará a implementação do método <xref:System.Web.ClientServices.Providers.IClientFormsAuthenticationCredentialsProvider.GetCredentials%2A?displayProperty=nameWithType>. Normalmente, você implementará este método para exibir uma caixa de diálogo e retornar um objeto <xref:System.Web.ClientServices.Providers.ClientFormsAuthenticationCredentials> populado.  
  
 Para obter mais informações sobre a autenticação, consulte [Autenticação do ASP.NET](http://msdn.microsoft.com/library/fc10b0ef-4ce4-4a7f-9174-886325221ee1). Para obter informações sobre como configurar o serviço de autenticação [!INCLUDE[ajax_current_short](../../../includes/ajax-current-short-md.md)], consulte [Usando formulários de autenticação com Microsoft Ajax](http://msdn.microsoft.com/library/c50f7dc5-323c-4c63-b4f3-96edfc1e815e).  
  
## <a name="roles"></a>Funções  
 Você pode usar serviços de aplicativos cliente para recuperar informações de função de um serviço de funções [!INCLUDE[ajax_current_short](../../../includes/ajax-current-short-md.md)]. Para determinar se usuário autenticado atual está em uma função específica, você chama o método <xref:System.Security.Principal.IPrincipal.IsInRole%2A> da referência <xref:System.Security.Principal.IPrincipal> recuperada da propriedade `static` <xref:System.Threading.Thread.CurrentPrincipal%2A?displayProperty=nameWithType>. O método <xref:System.Security.Principal.IPrincipal.IsInRole%2A> usa o nome da função como um parâmetro e retorna um valor <xref:System.Boolean> que indica se o usuário atual está na função especificada. Este método retornará `false` se o usuário não estiver autenticado ou não estiver na função especificada.  
  
 Para obter informações sobre como configurar o serviço [!INCLUDE[ajax_current_short](../../../includes/ajax-current-short-md.md)], consulte [Usando funções de informações com Microsoft Ajax](http://msdn.microsoft.com/library/280f6ad9-ba1a-4fc9-b0cc-22e39e54a82d).  
  
## <a name="settings"></a>Configurações  
 Você pode usar serviços de aplicativos cliente para recuperar configurações de aplicativo do usuário de um serviço de perfil [!INCLUDE[ajax_current_short](../../../includes/ajax-current-short-md.md)] existente. O recurso de configurações da Web dos serviços de aplicativos cliente se integra ao recurso de configurações de aplicativo fornecido em [!INCLUDE[dnprdnlong](../../../includes/dnprdnlong-md.md)]. Para recuperar as configurações da Web, primeiro gere uma classe `Settings` (acessada como `Properties.Settings.Default` no C# e `My.Settings` em [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]) para seu projeto usando a guia **Configurações** do designer de projeto [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)]. Na guia **Configurações**, você pode usar o botão **Carregar Configurações da Web** para recuperar as configurações da Web e adicioná-las à classe `Settings` gerada. Você pode usar as configurações da Web configuradas para uso por todos os usuários autenticados ou todos os usuários anônimos.  
  
 Para obter mais informações sobre as configurações de aplicativo, consulte [Visão geral sobre configurações de aplicativo](../../../docs/framework/winforms/advanced/application-settings-overview.md). Para obter informações sobre como implementar sua própria classe de configurações em vez de gerar uma no [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)], consulte [How to: Create Application Settings](../../../docs/framework/winforms/advanced/how-to-create-application-settings.md) (Como criar configurações de aplicativo). Para obter informações sobre como configurar o serviço de perfil [!INCLUDE[ajax_current_short](../../../includes/ajax-current-short-md.md)], consulte [Usando perfis de informações com Microsoft Ajax](http://msdn.microsoft.com/library/91239ae6-d01c-4f4e-a433-eb9040dbed61).  
  
## <a name="client-application-services-classes"></a>Classes de serviços de aplicativos cliente  
 A tabela a seguir descreve as classes que implementam o recurso de serviços de aplicativos cliente.  
  
 Aplicativos que usam apenas a autenticação primária, funções e recursos de configurações não terão acesso a essas classes diretamente. Em vez disso, esses aplicativos poderão acessar os provedores de serviços de aplicativos cliente indiretamente usando a configuração do aplicativo e as APIs descritas nas seções anteriores. Você acessará essas classes diretamente para implementar recursos adicionais, como o logout do usuário e a funcionalidade offline.  
  
> [!NOTE]
>  Todas as APIs de serviços de aplicativos cliente são síncronas. Os serviços de aplicativos cliente não dão suporte diretamente ao comportamento assíncrono.  
  
 Os provedores de serviço de aplicativos cliente implementam ou estendem os tipos [!INCLUDE[dnprdnlong](../../../includes/dnprdnlong-md.md)] padrão, mas não implementam todos os membros e recursos definidos por esses tipos. Por exemplo, você não pode usar os provedores de serviço de aplicativos cliente para implementar um aplicativo de gerenciamento de usuários para criar novos usuários e gerenciar a associação de função. Para implementar essa funcionalidade, atualmente você deve usar um aplicativo Web e o código do lado do servidor. Para determinar quais membros não são implementados, consulte a documentação de referência, que você pode acessar pelos links nesta tabela.  
  
|Classe|Descrição|  
|-----------|-----------------|  
|<xref:System.Web.ClientServices.ClientFormsIdentity>|Essa classe gerencia os cookies de autenticação e identidade do usuário para autenticação de formulários.<br /><br /> O principal motivo para acessar essa classe diretamente é chamar o método <xref:System.Web.ClientServices.ClientFormsIdentity.RevalidateUser%2A>, que silenciosamente revalidada um usuário (por exemplo, quando você alterna do modo offline para online).<br /><br /> Depois que o usuário é autenticado usando a autenticação de formulários, você pode recuperar uma instância dessa classe através da propriedade <xref:System.Security.Principal.IPrincipal.Identity%2A> da referência <xref:System.Security.Principal.IPrincipal> recuperada por meio da propriedade `static` <xref:System.Threading.Thread.CurrentPrincipal%2A?displayProperty=nameWithType>.|  
|<xref:System.Web.ClientServices.ClientRolePrincipal>|Essa classe gerencia as funções de usuário.<br /><br /> Essa classe não tem nenhum membro que não possa ser acessado indiretamente. No entanto, depois que o usuário é autenticado, você pode acessar uma instância dessa classe por meio da propriedade `static` <xref:System.Threading.Thread.CurrentPrincipal%2A?displayProperty=nameWithType>.|  
|<xref:System.Web.ClientServices.ConnectivityStatus>|Essa classe fornece a propriedade `static` <xref:System.Web.ClientServices.ConnectivityStatus.IsOffline%2A> que você pode usar para alternar o aplicativo para o modo offline.|  
|<xref:System.Web.ClientServices.Providers.ClientFormsAuthenticationCredentials>|Essa classe representa as credenciais do usuário.<br /><br /> Você usará essa classe apenas como o tipo de valor retornado do método <xref:System.Web.ClientServices.Providers.IClientFormsAuthenticationCredentialsProvider.GetCredentials%2A> ao implementar a interface <xref:System.Web.ClientServices.Providers.IClientFormsAuthenticationCredentialsProvider>.|  
|<xref:System.Web.ClientServices.Providers.ClientFormsAuthenticationMembershipProvider>|Essa classe gerencia o acesso ao serviço de autenticação remota para autenticação de formulários.<br /><br /> O principal motivo para acessar essa classe diretamente é para usar seus membros <xref:System.Web.ClientServices.Providers.ClientFormsAuthenticationMembershipProvider.Logout%2A> e <xref:System.Web.ClientServices.Providers.ClientFormsAuthenticationMembershipProvider.UserValidated>, que não são implementados pela classe <xref:System.Web.Security.MembershipProvider> base. Você também pode definir o local do serviço por meio de programação usando a propriedade <xref:System.Web.ClientServices.Providers.ClientFormsAuthenticationMembershipProvider.ServiceUri%2A>.<br /><br /> Você pode recuperar uma instância dessa classe através da propriedade `static` <xref:System.Web.Security.Membership.Provider%2A?displayProperty=nameWithType>.|  
|<xref:System.Web.ClientServices.Providers.ClientWindowsAuthenticationMembershipProvider>|Essa classe gerencia a autenticação do Windows.<br /><br /> O principal motivo para acessar essa classe diretamente é chamar seu método <xref:System.Web.ClientServices.Providers.ClientWindowsAuthenticationMembershipProvider.Logout%2A>. Após o logout, o usuário ainda será autenticado para o Windows, mas não poderá acessar os serviços de aplicativo remotos.<br /><br /> Você pode recuperar uma instância dessa classe através da propriedade `static` <xref:System.Web.Security.Membership.Provider%2A?displayProperty=nameWithType>.|  
|<xref:System.Web.ClientServices.Providers.ClientRoleProvider>|Essa classe gerencia o acesso ao serviço de funções remoto.<br /><br /> O principal motivo para acessar essa classe é chamar seu método <xref:System.Web.ClientServices.Providers.ClientRoleProvider.ResetCache%2A>. Isso poderá ser útil se seu aplicativo estiver configurado para usar um valor de tempo limite de cache de serviço de função diferente de zero. Para obter mais informações, consulte [Como configurar serviços de aplicativo cliente](../../../docs/framework/common-client-technologies/how-to-configure-client-application-services.md). Você também pode definir o local do serviço por meio de programação usando a propriedade <xref:System.Web.ClientServices.Providers.ClientRoleProvider.ServiceUri%2A>.<br /><br /> Você pode recuperar uma instância dessa classe através da propriedade `static` <xref:System.Web.Security.Roles.Provider%2A?displayProperty=nameWithType>.|  
|<xref:System.Web.ClientServices.Providers.ClientSettingsProvider>|Essa classe gerencia o acesso ao serviço configurações da Web remoto.<br /><br /> O principal motivo para acessar essa classe é manipular o evento <xref:System.Web.ClientServices.Providers.ClientSettingsProvider.SettingsSaved>. Você também pode definir o local do serviço por meio de programação usando a propriedade <xref:System.Web.ClientServices.Providers.ClientSettingsProvider.ServiceUri%2A>.|  
|<xref:System.Web.ClientServices.Providers.IClientFormsAuthenticationCredentialsProvider>|Essa interface fornece uma maneira indireta de seu aplicativo adquirir credenciais de usuário para validação, conforme descrito anteriormente na seção Autenticação desse tópico. Para obter mais informações, consulte [Como configurar serviços de aplicativo cliente](../../../docs/framework/common-client-technologies/how-to-configure-client-application-services.md).|  
|<xref:System.Web.ClientServices.Providers.SettingsSavedEventArgs>|Essa classe fornece uma propriedade <xref:System.Web.ClientServices.Providers.SettingsSavedEventArgs.FailedSettingsList%2A> para uso dentro de um manipulador de eventos <xref:System.Web.ClientServices.Providers.ClientSettingsProvider.SettingsSaved?displayProperty=nameWithType>.|  
|<xref:System.Web.ClientServices.Providers.UserValidatedEventArgs>|Essa classe fornece uma propriedade <xref:System.Web.ClientServices.Providers.UserValidatedEventArgs.UserName%2A> para uso dentro de um manipulador de eventos <xref:System.Web.ClientServices.Providers.ClientFormsAuthenticationMembershipProvider.UserValidated>.|  
  
## <a name="see-also"></a>Consulte também  
 [Serviços de aplicativos cliente](../../../docs/framework/common-client-technologies/client-application-services.md)  
 [Como configurar serviços de aplicativo cliente](../../../docs/framework/common-client-technologies/how-to-configure-client-application-services.md)  
 [Como implementar login de usuário com serviços de aplicativos cliente](../../../docs/framework/common-client-technologies/how-to-implement-user-login-with-client-application-services.md)  
 [Instruções passo a passo: usando serviços de aplicativos cliente](../../../docs/framework/common-client-technologies/walkthrough-using-client-application-services.md)  
 [Visão Geral das Configurações do Aplicativo](../../../docs/framework/winforms/advanced/application-settings-overview.md)  
 [Visão geral dos Serviços de Aplicativos ASP.NET](http://msdn.microsoft.com/library/1162e529-0d70-44b2-b3ab-83e60c695013)  
 [Usando formulários de autenticação com Microsoft Ajax](http://msdn.microsoft.com/library/c50f7dc5-323c-4c63-b4f3-96edfc1e815e)  
 [Usando informações de funções com o Microsoft Ajax](http://msdn.microsoft.com/library/280f6ad9-ba1a-4fc9-b0cc-22e39e54a82d)  
 [Usando informações de perfis com o Microsoft Ajax](http://msdn.microsoft.com/library/91239ae6-d01c-4f4e-a433-eb9040dbed61)  
 [Autenticação do ASP.NET](http://msdn.microsoft.com/library/fc10b0ef-4ce4-4a7f-9174-886325221ee1)  
 [Gerenciando a autorização usando funções](http://msdn.microsoft.com/library/01954ce4-39a2-487f-8153-a69f6f6f3195)  
 [Criando e configurando o banco de dados dos serviços de aplicativos para o SQL Server](http://msdn.microsoft.com/library/ab894e83-7e2f-4af8-a116-b1bff8f815b2)
