---
title: "Certificado de mensagem de segurança"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: WS Security
ms.assetid: 909333b3-35ec-48f0-baff-9a50161896f6
caps.latest.revision: "51"
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.openlocfilehash: 0587883a7f354ec03e3fd47ea362b93f006028ba
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/18/2017
---
# <a name="message-security-certificate"></a><span data-ttu-id="73eb4-102">Certificado de mensagem de segurança</span><span class="sxs-lookup"><span data-stu-id="73eb4-102">Message Security Certificate</span></span>
<span data-ttu-id="73eb4-103">Este exemplo demonstra como implementar um aplicativo que usa o WS-Security com autenticação de certificado x. 509 v3 para o cliente e requer a autenticação de servidor usando o certificado do servidor x. 509 v3.</span><span class="sxs-lookup"><span data-stu-id="73eb4-103">This sample demonstrates how to implement an application that uses WS-Security with X.509 v3 certificate authentication for the client and requires server authentication using the server's X.509 v3 certificate.</span></span> <span data-ttu-id="73eb4-104">Este exemplo usa as configurações padrão, de modo que todas as mensagens de aplicativo entre o cliente e servidor assinadas e criptografadas.</span><span class="sxs-lookup"><span data-stu-id="73eb4-104">This sample uses default settings such that all application messages between the client and server are signed and encrypted.</span></span> <span data-ttu-id="73eb4-105">Este exemplo se baseia o [WSHttpBinding](../../../../docs/framework/wcf/samples/wshttpbinding.md) e consiste em um programa de console de cliente e uma biblioteca de serviços hospedados pelo Internet Information Services (IIS).</span><span class="sxs-lookup"><span data-stu-id="73eb4-105">This sample is based on the [WSHttpBinding](../../../../docs/framework/wcf/samples/wshttpbinding.md) and consists of a client console program and a service library hosted by Internet Information Services (IIS).</span></span> <span data-ttu-id="73eb4-106">O serviço implementa um contrato que define um padrão de comunicação de solicitação-resposta.</span><span class="sxs-lookup"><span data-stu-id="73eb4-106">The service implements a contract that defines a request-reply communication pattern.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="73eb4-107">As instruções de procedimento e a compilação de configuração para este exemplo estão localizadas no final deste tópico.</span><span class="sxs-lookup"><span data-stu-id="73eb4-107">The setup procedure and build instructions for this sample are located at the end of this topic.</span></span>  
  
 <span data-ttu-id="73eb4-108">O exemplo demonstra o controle de autenticação usando configuração e como obter a identidade do chamador do contexto de segurança, como mostrado no código de exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="73eb4-108">The sample demonstrates controlling authentication by using configuration and how to obtain the caller’s identity from the security context, as shown in the following sample code.</span></span>  
  
```  
public class CalculatorService : ICalculator  
{  
    public string GetCallerIdentity()  
    {  
        // The client certificate is not mapped to a Windows identity by default.  
        // ServiceSecurityContext.PrimaryIdentity is populated based on the information  
        // in the certificate that the client used to authenticate itself to the service.  
        return ServiceSecurityContext.Current.PrimaryIdentity.Name;  
    }  
    ...  
}  
```  
  
 <span data-ttu-id="73eb4-109">O serviço expõe um ponto de extremidade para se comunicar com o serviço e um ponto de extremidade para expor o documento WSDL do serviço usando o protocolo WS-MetadataExchange, definido usando o arquivo de configuração (Web. config).</span><span class="sxs-lookup"><span data-stu-id="73eb4-109">The service exposes one endpoint for communicating with the service and one endpoint for exposing the service's WSDL document using the WS-MetadataExchange protocol, defined by using the configuration file (Web.config).</span></span> <span data-ttu-id="73eb4-110">O ponto de extremidade consiste em um endereço, uma ligação e um contrato.</span><span class="sxs-lookup"><span data-stu-id="73eb4-110">The endpoint consists of an address, a binding, and a contract.</span></span> <span data-ttu-id="73eb4-111">A associação está configurada com um padrão [ \<wsHttpBinding >](../../../../docs/framework/configure-apps/file-schema/wcf/wshttpbinding.md) elemento, que foi padronizado para usar segurança de mensagem.</span><span class="sxs-lookup"><span data-stu-id="73eb4-111">The binding is configured with a standard [\<wsHttpBinding>](../../../../docs/framework/configure-apps/file-schema/wcf/wshttpbinding.md) element, which defaults to using message security.</span></span> <span data-ttu-id="73eb4-112">Este exemplo define o `clientCredentialType` de atributo para o certificado para exigir autenticação de cliente.</span><span class="sxs-lookup"><span data-stu-id="73eb4-112">This sample sets the `clientCredentialType` attribute to Certificate to require client authentication.</span></span>  
  
```xml  
<system.serviceModel>  
    <protocolMapping>  
      <add scheme="http" binding="wsHttpBinding"/>  
    </protocolMapping>  
    <bindings>  
      <wsHttpBinding>  
        <!--   
        This configuration defines the security mode as Message and   
        the clientCredentialType as Certificate.  
        -->  
        <binding>  
          <security mode ="Message">  
            <message clientCredentialType="Certificate" />  
          </security>  
        </binding>  
      </wsHttpBinding>  
    </bindings>  
    <!--For debugging purposes set the includeExceptionDetailInFaults attribute to true-->  
    <behaviors>  
      <serviceBehaviors>  
        <behavior>  
          <serviceMetadata httpGetEnabled="True"/>  
          <serviceDebug includeExceptionDetailInFaults="False" />  
          <!--   
        The serviceCredentials behavior allows one to define a service certificate.  
        A service certificate is used by the service to authenticate itself to its clients and to provide message protection.  
        This configuration references the "localhost" certificate installed during the setup instructions.  
        -->  
          <serviceCredentials>  
            <serviceCertificate findValue="localhost" storeLocation="LocalMachine" storeName="My" x509FindType="FindBySubjectName" />  
            <clientCertificate>  
              <!--   
            Setting the certificateValidationMode to PeerOrChainTrust means that if the certificate   
            is in the user's Trusted People store, then it will be trusted without performing a  
            validation of the certificate's issuer chain. This setting is used here for convenience so that the   
            sample can be run without having to have certificates issued by a certification authority (CA).  
            This setting is less secure than the default, ChainTrust. The security implications of this   
            setting should be carefully considered before using PeerOrChainTrust in production code.   
            -->  
              <authentication certificateValidationMode="PeerOrChainTrust" />  
            </clientCertificate>  
          </serviceCredentials>  
        </behavior>  
      </serviceBehaviors>  
    </behaviors>  
  </system.serviceModel>  
```  
  
 <span data-ttu-id="73eb4-113">O comportamento Especifica as credenciais do serviço que são usadas quando o cliente autentica o serviço.</span><span class="sxs-lookup"><span data-stu-id="73eb4-113">The behavior specifies the service's credentials that are used when the client authenticates the service.</span></span> <span data-ttu-id="73eb4-114">O nome de assunto do certificado de servidor é especificado no `findValue` atributo o [ \<serviceCredentials >](../../../../docs/framework/configure-apps/file-schema/wcf/servicecredentials.md) elemento.</span><span class="sxs-lookup"><span data-stu-id="73eb4-114">The server certificate subject name is specified in the `findValue` attribute in the [\<serviceCredentials>](../../../../docs/framework/configure-apps/file-schema/wcf/servicecredentials.md) element.</span></span>  
  
```xml  
<!--For debugging purposes, set the includeExceptionDetailInFaults attribute to true.-->  
<behaviors>  
      <serviceBehaviors>  
        <behavior>  
          <serviceMetadata httpGetEnabled="True"/>  
          <serviceDebug includeExceptionDetailInFaults="False" />  
          <!--   
        The serviceCredentials behavior allows one to define a service certificate.  
        A service certificate is used by the service to authenticate itself to its clients and to provide message protection.  
        This configuration references the "localhost" certificate installed during the setup instructions.  
        -->  
          <serviceCredentials>  
            <serviceCertificate findValue="localhost" storeLocation="LocalMachine" storeName="My" x509FindType="FindBySubjectName" />  
            <clientCertificate>  
              <!--   
            Setting the certificateValidationMode to PeerOrChainTrust means that if the certificate   
            is in the user's Trusted People store, then it will be trusted without performing a  
            validation of the certificate's issuer chain. This setting is used here for convenience so that the   
            sample can be run without having to have certificates issued by a certification authority (CA).  
            This setting is less secure than the default, ChainTrust. The security implications of this   
            setting should be carefully considered before using PeerOrChainTrust in production code.   
            -->  
              <authentication certificateValidationMode="PeerOrChainTrust" />  
            </clientCertificate>  
          </serviceCredentials>  
        </behavior>  
      </serviceBehaviors>  
    </behaviors>  
```  
  
 <span data-ttu-id="73eb4-115">A configuração do ponto de extremidade cliente consiste em um endereço absoluto para o ponto de extremidade de serviço, a associação e o contrato.</span><span class="sxs-lookup"><span data-stu-id="73eb4-115">The client endpoint configuration consists of an absolute address for the service endpoint, the binding, and the contract.</span></span> <span data-ttu-id="73eb4-116">A ligação do cliente é configurado com o modo de segurança apropriadas e modo de autenticação.</span><span class="sxs-lookup"><span data-stu-id="73eb4-116">The client binding is configured with the appropriate security mode and authentication mode.</span></span> <span data-ttu-id="73eb4-117">Quando em execução em um cenário entre computadores, certifique-se de que o endereço do ponto de extremidade de serviço é alterado.</span><span class="sxs-lookup"><span data-stu-id="73eb4-117">When running in a cross-computer scenario, ensure that the service endpoint address is changed accordingly.</span></span>  
  
```xml  
<system.serviceModel>  
    <client>  
      <!-- Use a behavior to configure the client certificate to present to the service. -->  
      <endpoint address="http://localhost/servicemodelsamples/service.svc" binding="wsHttpBinding" bindingConfiguration="Binding1" behaviorConfiguration="ClientCertificateBehavior" contract="Microsoft.Samples.Certificate.ICalculator"/>  
    </client>  
  
    <bindings>  
      <wsHttpBinding>  
        <!--   
        This configuration defines the security mode as Message and   
        the clientCredentialType as Certificate.  
        -->  
        <binding name="Binding1">  
          <security mode="Message">  
            <message clientCredentialType="Certificate"/>  
          </security>  
        </binding>  
      </wsHttpBinding>  
    </bindings>  
...  
</system.serviceModel>  
```  
  
 <span data-ttu-id="73eb4-118">A implementação do cliente pode definir o certificado a ser usado, por meio do arquivo de configuração ou código.</span><span class="sxs-lookup"><span data-stu-id="73eb4-118">The client implementation can set the certificate to use, either through the configuration file or through code.</span></span> <span data-ttu-id="73eb4-119">O exemplo a seguir mostra como definir o certificado a ser usado no arquivo de configuração.</span><span class="sxs-lookup"><span data-stu-id="73eb4-119">The following sample shows how to set the certificate to use in the configuration file.</span></span>  
  
```xml  
<system.serviceModel>  
  ...  
  
<behaviors>  
      <endpointBehaviors>  
        <behavior name="ClientCertificateBehavior">  
          <!--   
        The clientCredentials behavior allows one to define a certificate to present to a service.  
        A certificate is used by a client to authenticate itself to the service and provide message integrity.  
        This configuration references the "client.com" certificate installed during the setup instructions.  
        -->  
          <clientCredentials>  
            <clientCertificate findValue="client.com" storeLocation="CurrentUser" storeName="My" x509FindType="FindBySubjectName"/>  
            <serviceCertificate>  
              <!--   
            Setting the certificateValidationMode to PeerOrChainTrust means that if the certificate   
            is in the user's Trusted People store, then it will be trusted without performing a  
            validation of the certificate's issuer chain. This setting is used here for convenience so that the   
            sample can be run without having to have certificates issued by a certificate authority (CA).  
            This setting is less secure than the default, ChainTrust. The security implications of this   
            setting should be carefully considered before using PeerOrChainTrust in production code.   
            -->  
              <authentication certificateValidationMode="PeerOrChainTrust"/>  
            </serviceCertificate>  
          </clientCredentials>  
        </behavior>  
      </endpointBehaviors>  
    </behaviors>  
  
</system.serviceModel>  
```  
  
 <span data-ttu-id="73eb4-120">O exemplo a seguir mostra como chamar o serviço em seu programa.</span><span class="sxs-lookup"><span data-stu-id="73eb4-120">The following sample shows how to call the service in your program.</span></span>  
  
```  
// Create a client.  
CalculatorClient client = new CalculatorClient();  
  
// Call the GetCallerIdentity service operation.  
Console.WriteLine(client.GetCallerIdentity());  
...  
//Closing the client gracefully closes the connection and cleans up resources.  
client.Close();  
```  
  
 <span data-ttu-id="73eb4-121">Quando você executar o exemplo, as respostas e solicitações de operação são exibidas na janela do console do cliente.</span><span class="sxs-lookup"><span data-stu-id="73eb4-121">When you run the sample, the operation requests and responses are displayed in the client console window.</span></span> <span data-ttu-id="73eb4-122">Pressione ENTER na janela do cliente para desligar o cliente.</span><span class="sxs-lookup"><span data-stu-id="73eb4-122">Press ENTER in the client window to shut down the client.</span></span>  
  
```  
CN=client.com  
Add(100,15.99) = 115.99  
Subtract(145,76.54) = 68.46  
Multiply(9,81.25) = 731.25  
Divide(22,7) = 3.14285714285714  
Press <ENTER> to terminate client.  
```  
  
 <span data-ttu-id="73eb4-123">Arquivo em lotes bat incluído com os exemplos de segurança de mensagem permite que você configure o cliente e o servidor com certificados relevantes para executar um aplicativo hospedado que exige a segurança baseada em certificado.</span><span class="sxs-lookup"><span data-stu-id="73eb4-123">The Setup.bat batch file included with the Message Security samples enables you to configure the client and server with relevant certificates to run a hosted application that requires certificate-based security.</span></span> <span data-ttu-id="73eb4-124">O arquivo em lotes pode ser executado em três modos.</span><span class="sxs-lookup"><span data-stu-id="73eb4-124">The batch file can be run in three modes.</span></span> <span data-ttu-id="73eb4-125">Para ser executado no tipo de computador único modo **bat** em um Prompt de comando Visual Studio; para o tipo de modo de serviço **bat serviço**; e para o tipo de modo de cliente **bat cliente** .</span><span class="sxs-lookup"><span data-stu-id="73eb4-125">To run in single-computer mode type **setup.bat** in a Visual Studio Command Prompt ; for service mode type **setup.bat service**; and for client mode type **setup.bat client**.</span></span> <span data-ttu-id="73eb4-126">Use o modo de cliente e servidor ao executar a amostra entre computadores.</span><span class="sxs-lookup"><span data-stu-id="73eb4-126">Use the client and server mode when running the sample across computers.</span></span> <span data-ttu-id="73eb4-127">Consulte o procedimento de instalação no final deste tópico para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="73eb4-127">See the setup procedure at the end of this topic for details.</span></span> <span data-ttu-id="73eb4-128">O exemplo a seguir fornece uma visão geral das seções diferentes dos arquivos de lote para que eles podem ser modificados para executar a configuração apropriada:</span><span class="sxs-lookup"><span data-stu-id="73eb4-128">The following provides a brief overview of the different sections of the batch files so that they can be modified to run in appropriate configuration:</span></span>  
  
-   <span data-ttu-id="73eb4-129">Criando o certificado de cliente.</span><span class="sxs-lookup"><span data-stu-id="73eb4-129">Creating the client certificate.</span></span>  
  
     <span data-ttu-id="73eb4-130">A seguinte linha no arquivo de lote cria o certificado de cliente.</span><span class="sxs-lookup"><span data-stu-id="73eb4-130">The following line in the batch file creates the client certificate.</span></span> <span data-ttu-id="73eb4-131">O nome do cliente especificado é usado no nome da entidade do certificado criado.</span><span class="sxs-lookup"><span data-stu-id="73eb4-131">The client name specified is used in the subject name of the certificate created.</span></span> <span data-ttu-id="73eb4-132">O certificado é armazenado no `My` armazenar no `CurrentUser` local do repositório.</span><span class="sxs-lookup"><span data-stu-id="73eb4-132">The certificate is stored in `My` store at the `CurrentUser` store location.</span></span>  
  
    ```  
    echo ************  
    echo making client cert  
    echo ************  
    makecert.exe -sr CurrentUser -ss MY -a sha1 -n CN=%CLIENT_NAME% -sky exchange -pe  
    ```  
  
-   <span data-ttu-id="73eb4-133">Instalando o certificado de cliente no repositório de certificados confiáveis do servidor.</span><span class="sxs-lookup"><span data-stu-id="73eb4-133">Installing the client certificate into the server’s trusted certificate store.</span></span>  
  
     <span data-ttu-id="73eb4-134">A seguinte linha nas cópias do arquivo em lotes o certificado cliente TrustedPeople do servidor armazenar para que o servidor possa fazer a confiança relevante ou decisões não confiáveis.</span><span class="sxs-lookup"><span data-stu-id="73eb4-134">The following line in the batch file copies the client certificate into the server's TrustedPeople store so that the server can make the relevant trust or no-trust decisions.</span></span> <span data-ttu-id="73eb4-135">Em ordem para um certificado instalado no repositório de TrustedPeople para ser confiável por um [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] o modo de validação de certificado de cliente de serviço, deve ser definido como `PeerOrChainTrust` ou `PeerTrust`.</span><span class="sxs-lookup"><span data-stu-id="73eb4-135">In order for a certificate installed in the TrustedPeople store to be trusted by a [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] service, the client certificate validation mode must be set to `PeerOrChainTrust` or `PeerTrust`.</span></span> <span data-ttu-id="73eb4-136">Consulte o exemplo de configuração de serviço anterior para saber como isso pode ser feito usando um arquivo de configuração.</span><span class="sxs-lookup"><span data-stu-id="73eb4-136">See the previous service configuration sample to learn how this can be done by using a configuration file.</span></span>  
  
    ```  
    echo ************  
    echo copying client cert to server's LocalMachine store  
    echo ************  
    certmgr.exe -add -r CurrentUser -s My -c -n %CLIENT_NAME% -r LocalMachine -s TrustedPeople   
    ```  
  
-   <span data-ttu-id="73eb4-137">Criando o certificado do servidor.</span><span class="sxs-lookup"><span data-stu-id="73eb4-137">Creating the server certificate.</span></span>  
  
     <span data-ttu-id="73eb4-138">As seguintes linhas do arquivo em lotes bat criam o certificado do servidor a ser usado.</span><span class="sxs-lookup"><span data-stu-id="73eb4-138">The following lines from the Setup.bat batch file create the server certificate to be used.</span></span>  
  
    ```  
    echo ************  
    echo Server cert setup starting  
    echo %SERVER_NAME%  
    echo ************  
    echo making server cert  
    echo ************  
    makecert.exe -sr LocalMachine -ss MY -a sha1 -n CN=%SERVER_NAME% -sky exchange -pe  
    ```  
  
     <span data-ttu-id="73eb4-139">A variável % SERVER_NAME % Especifica o nome do servidor.</span><span class="sxs-lookup"><span data-stu-id="73eb4-139">The %SERVER_NAME% variable specifies the server name.</span></span> <span data-ttu-id="73eb4-140">O certificado é armazenado no repositório de LocalMachine.</span><span class="sxs-lookup"><span data-stu-id="73eb4-140">The certificate is stored in the LocalMachine store.</span></span> <span data-ttu-id="73eb4-141">Se o arquivo em lotes bat é executado com um argumento de serviço (como **bat serviço**) % SERVER_NAME % contém o nome de domínio totalmente qualificado do computador.</span><span class="sxs-lookup"><span data-stu-id="73eb4-141">If the Setup.bat batch file is run with an argument of service (such as, **setup.bat service**) the %SERVER_NAME% contains the fully-qualified domain name of the computer.</span></span> <span data-ttu-id="73eb4-142">Caso contrário, o padrão é localhost.</span><span class="sxs-lookup"><span data-stu-id="73eb4-142">Otherwise it defaults to localhost.</span></span>  
  
-   <span data-ttu-id="73eb4-143">Instalando o certificado de servidor no repositório de certificados confiáveis do cliente.</span><span class="sxs-lookup"><span data-stu-id="73eb4-143">Installing the server certificate into the client’s trusted certificate store.</span></span>  
  
     <span data-ttu-id="73eb4-144">A linha a seguir copia o certificado do servidor para o armazenamento de pessoas confiáveis do cliente.</span><span class="sxs-lookup"><span data-stu-id="73eb4-144">The following line copies the server certificate into the client trusted people store.</span></span> <span data-ttu-id="73eb4-145">Esta etapa é necessária porque os certificados gerados pela Makecert.exe não são implicitamente confiáveis pelo sistema do cliente.</span><span class="sxs-lookup"><span data-stu-id="73eb4-145">This step is required because certificates generated by Makecert.exe are not implicitly trusted by the client system.</span></span> <span data-ttu-id="73eb4-146">Se você já tiver um certificado que está enraizado em um certificado de raiz confiável do cliente — por exemplo, um certificado emitido Microsoft — essa etapa de preenchimento do repositório de certificados de cliente com o certificado do servidor não é necessária.</span><span class="sxs-lookup"><span data-stu-id="73eb4-146">If you already have a certificate that is rooted in a client trusted root certificate—for example, a Microsoft-issued certificate—this step of populating the client certificate store with the server certificate is not required.</span></span>  
  
    ```  
    certmgr.exe -add -r LocalMachine -s My -c -n %SERVER_NAME% -r CurrentUser -s TrustedPeople  
    ```  
  
-   <span data-ttu-id="73eb4-147">Concedendo permissões de chave privada do certificado.</span><span class="sxs-lookup"><span data-stu-id="73eb4-147">Granting permissions on the certificate's private key.</span></span>  
  
     <span data-ttu-id="73eb4-148">As seguintes linhas no arquivo bat Verifique o certificado de servidor armazenado no repositório de LocalMachine acessível para o [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] conta de processo do operador.</span><span class="sxs-lookup"><span data-stu-id="73eb4-148">The following lines in the Setup.bat file make the server certificate stored in the LocalMachine store accessible to the [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] worker process account.</span></span>  
  
    ```  
    echo ************  
    echo setting privileges on server certificates  
    echo ************  
    for /F "delims=" %%i in ('"%ProgramFiles%\ServiceModelSampleTools\FindPrivateKey.exe" My LocalMachine -n CN^=%SERVER_NAME% -a') do set PRIVATE_KEY_FILE=%%i  
    set WP_ACCOUNT=NT AUTHORITY\NETWORK SERVICE  
    (ver | findstr /C:"5.1") && set WP_ACCOUNT=%COMPUTERNAME%\ASPNET  
    echo Y|cacls.exe "%PRIVATE_KEY_FILE%" /E /G "%WP_ACCOUNT%":R  
    iisreset  
    ```  
  
    > [!NOTE]
    >  <span data-ttu-id="73eb4-149">Se você estiver usando um fora dos EUA Edição em inglês do Windows, você deve editar o BAT arquivo e substitua o nome da conta "NT AUTHORITY\NETWORK SERVICE" por seu equivalente regional.</span><span class="sxs-lookup"><span data-stu-id="73eb4-149">If you are using a non-U.S. English edition of Windows, you must edit the Setup.bat file and replace the "NT AUTHORITY\NETWORK SERVICE" account name with your regional equivalent.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="73eb4-150">As ferramentas usadas nesse arquivo em lotes estão localizadas em C:\Program Files\Microsoft Visual Studio 8 \ Common7\Tools ou C:\Program Files\Microsoft SDKs\Windows\v6.0\bin.</span><span class="sxs-lookup"><span data-stu-id="73eb4-150">The tools used in this batch file are located in either C:\Program Files\Microsoft Visual Studio 8\Common7\tools or C:\Program Files\Microsoft SDKs\Windows\v6.0\bin.</span></span> <span data-ttu-id="73eb4-151">Um desses diretórios deve estar no caminho do sistema.</span><span class="sxs-lookup"><span data-stu-id="73eb4-151">One of these directories must be in your system path.</span></span> <span data-ttu-id="73eb4-152">Se você tiver instalado o Visual Studio, a maneira mais fácil de obter esse diretório no caminho é abrir o Prompt de comando do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="73eb4-152">If you have Visual Studio installed, the easiest way to get this directory in your path is to open the Visual Studio Command Prompt.</span></span> <span data-ttu-id="73eb4-153">Clique em **iniciar**e, em seguida, selecione **todos os programas**, **Visual Studio 2012**, **ferramentas**.</span><span class="sxs-lookup"><span data-stu-id="73eb4-153">Click **Start**, and then select **All Programs**, **Visual Studio 2012**, **Tools**.</span></span> <span data-ttu-id="73eb4-154">Esse prompt de comando tem os caminhos apropriados já configurados.</span><span class="sxs-lookup"><span data-stu-id="73eb4-154">This command prompt has the appropriate paths already configured.</span></span> <span data-ttu-id="73eb4-155">Caso contrário, você deve adicionar o diretório apropriado para seu caminho manualmente.</span><span class="sxs-lookup"><span data-stu-id="73eb4-155">Otherwise you must add the appropriate directory to your path manually.</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="73eb4-156">Os exemplos podem mais ser instalados no seu computador.</span><span class="sxs-lookup"><span data-stu-id="73eb4-156">The samples may already be installed on your computer.</span></span> <span data-ttu-id="73eb4-157">Verificar o seguinte diretório (padrão) antes de continuar:</span><span class="sxs-lookup"><span data-stu-id="73eb4-157">Check for the following (default) directory before continuing:</span></span>  
>   
>  `<InstallDrive>:\WF_WCF_Samples`  
>   
>  <span data-ttu-id="73eb4-158">Se este diretório não existir, vá para [Windows Communication Foundation (WCF) e exemplos do Windows Workflow Foundation (WF) para o .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) para baixar todos os [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)] exemplos.</span><span class="sxs-lookup"><span data-stu-id="73eb4-158">If this directory does not exist, go to [Windows Communication Foundation (WCF) and Windows Workflow Foundation (WF) Samples for .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) to download all [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] and [!INCLUDE[wf1](../../../../includes/wf1-md.md)] samples.</span></span> <span data-ttu-id="73eb4-159">Este exemplo está no seguinte diretório:</span><span class="sxs-lookup"><span data-stu-id="73eb4-159">This sample is located in the following directory:</span></span>  
>   
>  `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Binding\WS\MessageSecurity`  
  
### <a name="to-set-up-build-and-run-the-sample"></a><span data-ttu-id="73eb4-160">Para configurar, compilar, e executar o exemplo</span><span class="sxs-lookup"><span data-stu-id="73eb4-160">To set up, build, and run the sample</span></span>  
  
1.  <span data-ttu-id="73eb4-161">Certifique-se de que você executou o [único procedimento de instalação para os exemplos do Windows Communication Foundation](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).</span><span class="sxs-lookup"><span data-stu-id="73eb4-161">Ensure that you have performed the [One-Time Setup Procedure for the Windows Communication Foundation Samples](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).</span></span>  
  
2.  <span data-ttu-id="73eb4-162">Para compilar o c# ou Visual Basic .NET edição da solução, siga as instruções em [compilar os exemplos do Windows Communication Foundation](../../../../docs/framework/wcf/samples/building-the-samples.md).</span><span class="sxs-lookup"><span data-stu-id="73eb4-162">To build the C# or Visual Basic .NET edition of the solution, follow the instructions in [Building the Windows Communication Foundation Samples](../../../../docs/framework/wcf/samples/building-the-samples.md).</span></span>  
  
### <a name="to-run-the-sample-on-the-same-computer"></a><span data-ttu-id="73eb4-163">Para executar o exemplo no mesmo computador</span><span class="sxs-lookup"><span data-stu-id="73eb4-163">To run the sample on the same computer</span></span>  
  
1.  <span data-ttu-id="73eb4-164">Abra um Prompt de comando do Visual Studio com privilégios de administrador e execute bat da pasta de instalação do exemplo.</span><span class="sxs-lookup"><span data-stu-id="73eb4-164">Open a Visual Studio Command Prompt  with administrator privileges and run Setup.bat from the sample install folder.</span></span> <span data-ttu-id="73eb4-165">Isso instala todos os certificados necessários para executar o exemplo.</span><span class="sxs-lookup"><span data-stu-id="73eb4-165">This installs all the certificates required for running the sample.</span></span>  
  
    > [!NOTE]
    >  <span data-ttu-id="73eb4-166">O arquivo em lotes bat foi projetado para ser executado a partir de um Prompt de comando Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="73eb4-166">The Setup.bat batch file is designed to be run from a Visual Studio Command Prompt .</span></span> <span data-ttu-id="73eb4-167">Isso requer que a variável de ambiente path apontar para o diretório onde o SDK está instalado.</span><span class="sxs-lookup"><span data-stu-id="73eb4-167">It requires that the path environment variable point to the directory where the SDK is installed.</span></span> <span data-ttu-id="73eb4-168">Essa variável de ambiente é definida automaticamente dentro de um Visual Studio Command Prompt (2010).</span><span class="sxs-lookup"><span data-stu-id="73eb4-168">This environment variable is automatically set within a Visual Studio Command Prompt (2010).</span></span>  
  
2.  <span data-ttu-id="73eb4-169">Verifique se o acesso ao serviço usando um navegador inserindo o endereço `http://localhost/servicemodelsamples/service.svc`.</span><span class="sxs-lookup"><span data-stu-id="73eb4-169">Verify access to the service using a browser by entering the address `http://localhost/servicemodelsamples/service.svc`.</span></span>  
  
3.  <span data-ttu-id="73eb4-170">Inicie Client.exe de \Client\Bin.</span><span class="sxs-lookup"><span data-stu-id="73eb4-170">Launch Client.exe from \client\bin.</span></span> <span data-ttu-id="73eb4-171">Atividade do cliente é exibida no aplicativo de console do cliente.</span><span class="sxs-lookup"><span data-stu-id="73eb4-171">Client activity is displayed on the client console application.</span></span>  
  
4.  <span data-ttu-id="73eb4-172">Se o cliente e o serviço não for capazes de se comunicar, consulte [dicas de solução de problemas](http://msdn.microsoft.com/en-us/8787c877-5e96-42da-8214-fa737a38f10b).</span><span class="sxs-lookup"><span data-stu-id="73eb4-172">If the client and service are not able to communicate, see [Troubleshooting Tips](http://msdn.microsoft.com/en-us/8787c877-5e96-42da-8214-fa737a38f10b).</span></span>  
  
### <a name="to-run-the-sample-across-computers"></a><span data-ttu-id="73eb4-173">Para executar o exemplo em computadores</span><span class="sxs-lookup"><span data-stu-id="73eb4-173">To run the sample across computers</span></span>  
  
1.  <span data-ttu-id="73eb4-174">Crie um diretório no computador de serviço.</span><span class="sxs-lookup"><span data-stu-id="73eb4-174">Create a directory on the service computer.</span></span> <span data-ttu-id="73eb4-175">Crie um aplicativo virtual denominado servicemodelsamples para este diretório usando a ferramenta de gerenciamento de serviços de informações da Internet (IIS).</span><span class="sxs-lookup"><span data-stu-id="73eb4-175">Create a virtual application named servicemodelsamples for this directory by using the Internet Information Services (IIS) management tool.</span></span>  
  
2.  <span data-ttu-id="73eb4-176">Copie os arquivos de programa do serviço de \inetpub\wwwroot\servicemodelsamples para o diretório virtual no computador de serviço.</span><span class="sxs-lookup"><span data-stu-id="73eb4-176">Copy the service program files from \inetpub\wwwroot\servicemodelsamples to the virtual directory on the service computer.</span></span> <span data-ttu-id="73eb4-177">Certifique-se de que você copiar os arquivos no subdiretório \bin.</span><span class="sxs-lookup"><span data-stu-id="73eb4-177">Ensure that you copy the files in the \bin subdirectory.</span></span> <span data-ttu-id="73eb4-178">Também copie os arquivos. bat, Cleanup.bat e ImportClientCert.bat para o computador do serviço.</span><span class="sxs-lookup"><span data-stu-id="73eb4-178">Also copy the Setup.bat, Cleanup.bat, and ImportClientCert.bat files to the service computer.</span></span>  
  
3.  <span data-ttu-id="73eb4-179">Crie um diretório no computador cliente para os binários do cliente.</span><span class="sxs-lookup"><span data-stu-id="73eb4-179">Create a directory on the client computer for the client binaries.</span></span>  
  
4.  <span data-ttu-id="73eb4-180">Copie os arquivos de programa do cliente para o diretório de cliente no computador cliente.</span><span class="sxs-lookup"><span data-stu-id="73eb4-180">Copy the client program files to the client directory on the client computer.</span></span> <span data-ttu-id="73eb4-181">Também copie os arquivos. bat, Cleanup.bat e ImportServiceCert.bat ao cliente.</span><span class="sxs-lookup"><span data-stu-id="73eb4-181">Also copy the Setup.bat, Cleanup.bat, and ImportServiceCert.bat files to the client.</span></span>  
  
5.  <span data-ttu-id="73eb4-182">No servidor, execute **bat serviço** em um prompt de comando do Visual Studio com privilégios de administrador.</span><span class="sxs-lookup"><span data-stu-id="73eb4-182">On the server, run **setup.bat service** in a Visual Studio command prompt with administrator privileges.</span></span> <span data-ttu-id="73eb4-183">Executando **bat** com o **service** argumento cria um certificado de serviço com o nome de domínio totalmente qualificado do computador e exporta o certificado de serviço para um arquivo chamado Service.cer.</span><span class="sxs-lookup"><span data-stu-id="73eb4-183">Running **setup.bat** with the **service** argument creates a service certificate with the fully-qualified domain name of the computer and exports the service certificate to a file named Service.cer.</span></span>  
  
6.  <span data-ttu-id="73eb4-184">Editar o Web. config para refletir o novo nome de certificado (no `findValue` atributo o [ \<serviceCertificate >](../../../../docs/framework/configure-apps/file-schema/wcf/servicecertificate-of-servicecredentials.md)) que é o mesmo que o nome de domínio totalmente qualificado do computador.</span><span class="sxs-lookup"><span data-stu-id="73eb4-184">Edit Web.config to reflect the new certificate name (in the `findValue` attribute in the [\<serviceCertificate>](../../../../docs/framework/configure-apps/file-schema/wcf/servicecertificate-of-servicecredentials.md)) which is the same as the fully-qualified domain name of the computer.</span></span>  
  
7.  <span data-ttu-id="73eb4-185">Copie o arquivo de Service.cer do diretório de serviço para o diretório do cliente no computador cliente.</span><span class="sxs-lookup"><span data-stu-id="73eb4-185">Copy the Service.cer file from the service directory to the client directory on the client computer.</span></span>  
  
8.  <span data-ttu-id="73eb4-186">No cliente, execute **bat cliente** em um prompt de comando do Visual Studio com privilégios de administrador.</span><span class="sxs-lookup"><span data-stu-id="73eb4-186">On the client, run **setup.bat client** in a Visual Studio command prompt with administrator privileges.</span></span> <span data-ttu-id="73eb4-187">Executando **bat** com o **cliente** argumento cria um certificado de cliente chamado client.com e exporta o certificado de cliente para um arquivo chamado cer.</span><span class="sxs-lookup"><span data-stu-id="73eb4-187">Running **setup.bat** with the **client** argument creates a client certificate named client.com and exports the client certificate to a file named Client.cer.</span></span>  
  
9. <span data-ttu-id="73eb4-188">No arquivo Client.exe.config no computador cliente, altere o valor do endereço do ponto de extremidade para coincidir com o novo endereço do seu serviço.</span><span class="sxs-lookup"><span data-stu-id="73eb4-188">In the Client.exe.config file on the client computer, change the address value of the endpoint to match the new address of your service.</span></span> <span data-ttu-id="73eb4-189">Faça isso substituindo localhost com o nome de domínio totalmente qualificado do servidor.</span><span class="sxs-lookup"><span data-stu-id="73eb4-189">Do this by replacing localhost with the fully-qualified domain name of the server.</span></span>  
  
10. <span data-ttu-id="73eb4-190">Copie o arquivo CER do diretório do cliente para o diretório de serviço no servidor.</span><span class="sxs-lookup"><span data-stu-id="73eb4-190">Copy the Client.cer file from the client directory to the service directory on the server.</span></span>  
  
11. <span data-ttu-id="73eb4-191">No cliente, execute ImportServiceCert.bat em um prompt de comando do Visual Studio com privilégios administrativos.</span><span class="sxs-lookup"><span data-stu-id="73eb4-191">On the client, run ImportServiceCert.bat in a Visual Studio command prompt with administrative privileges.</span></span> <span data-ttu-id="73eb4-192">Isso importa o certificado de serviço do arquivo Service.cer para CurrentUser - TrustedPeople repositório.</span><span class="sxs-lookup"><span data-stu-id="73eb4-192">This imports the service certificate from the Service.cer file into the CurrentUser - TrustedPeople store.</span></span>  
  
12. <span data-ttu-id="73eb4-193">No servidor, execute ImportClientCert.bat em um prompt de comando do Visual Studio com privilégios administrativos.</span><span class="sxs-lookup"><span data-stu-id="73eb4-193">On the server, run ImportClientCert.bat in a Visual Studio command prompt with administrative privileges.</span></span> <span data-ttu-id="73eb4-194">Isso importa o certificado de cliente do arquivo CER para o repositório de LocalMachine - TrustedPeople.</span><span class="sxs-lookup"><span data-stu-id="73eb4-194">This imports the client certificate from the Client.cer file into the LocalMachine - TrustedPeople store.</span></span>  
  
13. <span data-ttu-id="73eb4-195">No computador cliente, inicie o Client.exe em uma janela de prompt de comando.</span><span class="sxs-lookup"><span data-stu-id="73eb4-195">On the client computer, launch Client.exe from a command prompt window.</span></span> <span data-ttu-id="73eb4-196">Se o cliente e o serviço não for capazes de se comunicar, consulte [dicas de solução de problemas](http://msdn.microsoft.com/en-us/8787c877-5e96-42da-8214-fa737a38f10b).</span><span class="sxs-lookup"><span data-stu-id="73eb4-196">If the client and service are not able to communicate, see [Troubleshooting Tips](http://msdn.microsoft.com/en-us/8787c877-5e96-42da-8214-fa737a38f10b).</span></span>  
  
### <a name="to-clean-up-after-the-sample"></a><span data-ttu-id="73eb4-197">A limpeza após a amostra</span><span class="sxs-lookup"><span data-stu-id="73eb4-197">To clean up after the sample</span></span>  
  
-   <span data-ttu-id="73eb4-198">Execute Cleanup.bat na pasta exemplos depois de terminar de executar o exemplo.</span><span class="sxs-lookup"><span data-stu-id="73eb4-198">Run Cleanup.bat in the samples folder after you have finished running the sample.</span></span>  
  
    > [!NOTE]
    >  <span data-ttu-id="73eb4-199">Esse script não remove os certificados de serviço em um cliente ao executar este exemplo entre computadores.</span><span class="sxs-lookup"><span data-stu-id="73eb4-199">This script does not remove service certificates on a client when running this sample across computers.</span></span> <span data-ttu-id="73eb4-200">Se você tiver executado [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] exemplos que usam certificados em computadores, certifique-se de desmarcar os certificados de serviço que foram instalados em CurrentUser - TrustedPeople repositório.</span><span class="sxs-lookup"><span data-stu-id="73eb4-200">If you have run [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] samples that use certificates across computers, be sure to clear the service certificates that have been installed in the CurrentUser - TrustedPeople store.</span></span> <span data-ttu-id="73eb4-201">Para fazer isso, use o seguinte comando: `certmgr -del -r CurrentUser -s TrustedPeople -c -n <Fully Qualified Server Machine Name>` por exemplo: `certmgr -del -r CurrentUser -s TrustedPeople -c -n server1.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="73eb4-201">To do this, use the following command: `certmgr -del -r CurrentUser -s TrustedPeople -c -n <Fully Qualified Server Machine Name>` For example: `certmgr -del -r CurrentUser -s TrustedPeople -c -n server1.contoso.com`.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="73eb4-202">Consulte também</span><span class="sxs-lookup"><span data-stu-id="73eb4-202">See Also</span></span>