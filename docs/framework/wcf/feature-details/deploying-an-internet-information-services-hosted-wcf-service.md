---
title: 部署承载于 Internet 信息服务中的 WCF 服务
ms.date: 03/30/2017
ms.assetid: 04ebd329-3fbd-44c3-b3ab-1de3517e27d7
ms.openlocfilehash: 59f18d8487deb52f5ecb5b5c814ec9bdbc74e2cc
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="deploying-an-internet-information-services-hosted-wcf-service"></a>部署承载于 Internet 信息服务中的 WCF 服务
开发和部署承载在 Internet 信息服务 (IIS) 的 Windows Communication Foundation (WCF) 服务包含以下任务：  
  
-   确保，IIS、 ASP.NET、 WCF 和 WCF 激活组件已正确安装并注册。  
  
-   创建新的 IIS 应用程序，或重新使用现有的 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 应用程序。  
  
-   创建 WCF 服务的.svc 文件。  
  
-   将服务实现部署到 IIS 应用程序。  
  
-   配置 WCF 服务。  
  
 有关创建承载于 IIS 中的 WCF 服务的详细演练，请参阅[如何： 承载在 IIS 中的 WCF 服务](../../../../docs/framework/wcf/feature-details/how-to-host-a-wcf-service-in-iis.md)。  
  
## <a name="ensure-that-iis-aspnet-and-wcf-are-correctly-installed-and-registered"></a>确保已正确安装和注册 IIS、ASP.NET 和 WCF  
 为 IIS 承载的 WCF 服务才能正常工作，必须安装 WCF、 IIS 和 ASP.NET。 安装 WCF 的过程 (作为的一部分[!INCLUDE[vstecwinfx](../../../../includes/vstecwinfx-md.md)])，ASP.NET 和 IIS 有所不同，具体取决于所使用的操作系统版本。 有关安装 WCF 的详细信息和[!INCLUDE[vstecwinfx](../../../../includes/vstecwinfx-md.md)]，请参阅[Microsoft.NET Framework 4 Web 安装程序](http://go.microsoft.com/fwlink/?LinkId=201185)。 有关安装 IIS 的说明可以在 [安装 IIS](http://go.microsoft.com/fwlink/?LinkId=201188)（可能为英文网页）上找到。  
  
 安装过程[!INCLUDE[vstecwinfx](../../../../includes/vstecwinfx-md.md)]如果 IIS 已存在，则在计算机上，自动向 IIS 注册 WCF。 如果之后安装 IIS [!INCLUDE[vstecwinfx](../../../../includes/vstecwinfx-md.md)]，向 IIS 注册 WCF 所需的一个额外的步骤和[!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)]。 根据您的操作系统，可以按如下所述执行此操作：  
  
-   [!INCLUDE[wxpsp2](../../../../includes/wxpsp2-md.md)]Windows 7 和[!INCLUDE[ws2003](../../../../includes/ws2003-md.md)]： 使用[ServiceModel 注册工具 (ServiceModelReg.exe)](../../../../docs/framework/wcf/servicemodelreg-exe.md)工具向 IIS 注册 WCF： 若要使用此工具，键入**ServiceModelReg.exe /i /x** Visual Studio 中命令提示符。 打开此命令提示符，方法是单击“开始”按钮、选择 **“所有程序”**, **“Microsoft Visual Studio 2012”**, **“Visual Studio 工具”**和 **“Visual Studio 命令提示符”**。  
  
-   [!INCLUDE[wv](../../../../includes/wv-md.md)]：安装 [!INCLUDE[vstecwinfx](../../../../includes/vstecwinfx-md.md)]的 Windows Communication Foundation Activation Components 子组件。 为此，请在控制面板中，单击**添加或删除程序**然后**添加\/删除 Windows 组件**。 这将激活 **“Windows 组件向导”**。  
  
-   Windows 7：  
  
 最后，必须确认已将 ASP.NET 配置为使用 .NET Framework 版本 4。 通过运行带 –i 选项的 ASPNET_Regiis 工具执行此操作。 有关详细信息，请参阅[ASP.NET IIS 注册工具](http://go.microsoft.com/fwlink/?LinkId=201186)  
  
## <a name="create-a-new-iis-application-or-reuse-an-existing-aspnet-application"></a>创建新的 IIS 应用程序或重新使用现有的 ASP.NET 应用程序  
 IIS 承载的 WCF 服务必须驻留在 IIS 应用程序内。 你可以以独占方式创建新的 IIS 应用程序承载 WCF 服务。 或者，你可以部署到现有应用程序现已承载的 WCF 服务[!INCLUDE[vstecasplong](../../../../includes/vstecasplong-md.md)]内容 （如.aspx 页和 ASP.NET Web 服务 [ASMX]）。 有关这些选项的详细信息，请参阅"托管 WCF-并排使用 ASP.NET"和"在 ASP.NET 兼容模式下承载 WCF 服务"部分中[WCF 服务和 ASP.NET](../../../../docs/framework/wcf/feature-details/wcf-services-and-aspnet.md)。  
  
 请注意， [!INCLUDE[iis601](../../../../includes/iis601-md.md)] 和更高版本定期重新启动独立的面向对象编程应用程序。 默认值为 1740 分钟。 支持的最大值为 71,582 分钟。 可以禁用此重新启动。 有关此属性的详细信息，请参阅[PeriodicRestartTime](http://go.microsoft.com/fwlink/?LinkId=109968)。  
  
## <a name="create-an-svc-file-for-the-wcf-service"></a>为 WCF 服务创建 .svc 文件  
 在 IIS 中承载的 WCF 服务表示为特殊内容文件 （.svc 文件） 对 IIS 应用程序中。 此模型与在 IIS 应用程序内将 ASMX 页表示为 .asmx 文件的方式类似。 .Svc 文件包含特定于 WCF 的处理指令 ([@ServiceHost](../../../../docs/framework/configure-apps/file-schema/wcf-directive/servicehost.md)) 允许 WCF 承载基础结构激活托管的服务以响应传入消息。 .svc 文件的最常见语法如以下语句所示。  
  
```  
<% @ServiceHost Service="MyNamespace.MyServiceImplementationTypeName" %>  
```  
  
 它由 [@ServiceHost](../../../../docs/framework/configure-apps/file-schema/wcf-directive/servicehost.md) 指令和单个属性 `Service`组成。 `Service` 属性的值是服务实现的公共语言运行库 (CLR) 类型名称。 使用此指令与使用以下代码创建服务主机基本等效。  
  
```  
new ServiceHost( typeof( MyNamespace.MyServiceImplementationTypeName ) );  
```  
  
 也可以执行其他承载配置，如创建服务的基址列表。 也可以使用自定义 <xref:System.ServiceModel.Activation.ServiceHostFactory> 扩展指令以用于自定义承载解决方案。 承载 WCF 服务的 IIS 应用程序不负责管理的创建和生存期的<xref:System.ServiceModel.ServiceHost>实例。 托管的 WCF 宿主基础结构创建必需<xref:System.ServiceModel.ServiceHost>收到.svc 文件的第一个请求时动态实例。 在代码显式关闭该实例之前或回收应用程序时，不释放该实例。  
  
 有关.svc 文件语法的详细信息，请参阅[ @ServiceHost ](../../../../docs/framework/configure-apps/file-schema/wcf-directive/servicehost.md)。  
  
## <a name="deploy-the-service-implementation-to-the-iis-application"></a>将服务实现部署到 IIS 应用程序  
 在 IIS 中承载的 WCF 服务使用相同的动态编译模型[!INCLUDE[vstecasplong](../../../../includes/vstecasplong-md.md)]。 正如使用[!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)]，你可以部署在各种位置，有几个方面的 IIS 承载的 WCF 服务的实现代码，如下所示：  
  
-   作为全局程序集缓存 (GAC) 或应用程序的 \bin 目录中的预编译 .dll 文件。 在部署类库的新版本后，才更新预编译的二进制文件。  
  
-   作为位于应用程序的 \App_Code 目录中的未编译源文件。 处理应用程序的第一个请求时，动态需要位于此目录中的源文件。 对 \App_Code 目录中文件进行的任何更改都导致在收到下一个请求时回收和重新编译整个应用程序。  
  
-   作为直接放置在 .svc 文件中的未编译代码。 实现代码也可以按内联方式位于的服务的.svc 文件之后,@ServiceHost指令。 对内联代码进行的任何更改导致在收到下一个请求时回收和重新编译应用程序。  
  
 有关详细信息[!INCLUDE[vstecasplong](../../../../includes/vstecasplong-md.md)]编译模型，请参阅[ASP.NET 编译概述](http://go.microsoft.com/fwlink/?LinkId=94773)。  
  
## <a name="configure-the-wcf-service"></a>配置 WCF 服务  
 IIS 承载的 WCF 服务将其配置存储在应用程序 Web.config 文件中。 IIS 承载的服务使用与在 IIS 外部承载的 WCF 服务相同的配置元素和语法。 但是，下面的约束对 IIS 承载环境是唯一的：  
  
-   承载于 IIS 中的服务的基址。  
  
-   在 IIS 外部承载的 WCF 服务可以控制他们通过传递一组基托管的服务的基址的应用程序地址 Uri 对<xref:System.ServiceModel.ServiceHost>构造函数或通过提供[\<主机 >](../../../../docs/framework/configure-apps/file-schema/wcf/host.md)中的元素服务的配置。 承载于 IIS 中的服务无法控制其基址；承载于 IIS 中的服务的基址是其 .svc 文件的地址。  
  
### <a name="endpoint-addresses-for-iis-hosted-services"></a>承载于 IIS 中的服务的终结点地址  
 承载于 IIS 中时，任何终结点地址始终被认为相对于表示服务的 .svc 文件的地址。 例如，如果 WCF 服务的基址是http://localhost/Application1/MyService.svc使用以下终结点配置。  
  
```xml  
<endpoint address="anotherEndpoint" .../>  
```  
  
 这提供终结点，可以在达到"http://localhost/Application1/MyService.svc/anotherEndpoint"。  
  
 同样，使用空字符串，如提供在可访问终结点的相对地址的终结点配置元素http://localhost/Application1/MyService.svc，即的基址。  
  
```xml  
<endpoint address="" ... />  
```  
  
 对于承载于 IIS 中的服务的终结点，必须始终使用相对终结点地址。 提供完全限定的终结点地址 (例如，http://localhost/MyService.svc)如果终结点地址未指向承载公开终结点的服务 IIS 的应用程序可能会导致服务的部署中的错误。 对所承载的服务使用相对终结点地址避免了这些潜在冲突。  
  
### <a name="available-transports"></a>可用传输  
 WCF 服务承载于 IIS 5.1 和[!INCLUDE[iis601](../../../../includes/iis601-md.md)]被限制为使用基于 HTTP 的通信。 在这些 IIS 平台上，将所承载的服务配置为使用非 HTTP 绑定会导致服务激活期间出错。 对于 [!INCLUDE[iisver](../../../../includes/iisver-md.md)]，支持的传输包括 HTTP、Net.TCP、Net.Pipe、Net.MSMQ 以及用于与现有 MSMQ 应用程序向后兼容的 msmq.formatname。  
  
### <a name="http-transport-security"></a>HTTP 传输安全  
 IIS 承载的 WCF 服务可以使用 HTTP 传输安全 （例如，HTTPS 和 HTTP 身份验证方案，如基本、 摘要式和 Windows 集成身份验证），前提是包含该服务的 IIS 虚拟目录支持那些设置。 所承载终结点的绑定上的 HTTP 传输安全设置必须与包含它的 IIS 虚拟目录上的传输安全设置匹配。  
  
 例如，配置为使用 HTTP 摘要式身份验证的 WCF 终结点必须驻留在也配置为允许 HTTP 摘要式身份验证的 IIS 虚拟目录。 IIS 设置和 WCF 终结点设置不匹配的组合导致服务激活期间出错。  
  
## <a name="see-also"></a>请参阅  
 [在 Internet Information Services 中承载](../../../../docs/framework/wcf/feature-details/hosting-in-internet-information-services.md)  
 [Internet Information Services 承载最佳做法](../../../../docs/framework/wcf/feature-details/internet-information-services-hosting-best-practices.md)  
 [Windows Server App Fabric 承载功能](http://go.microsoft.com/fwlink/?LinkId=201276)
