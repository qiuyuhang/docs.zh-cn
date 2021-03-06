---
title: 发现绑定元素示例
ms.date: 03/30/2017
ms.assetid: af513015-85bf-417b-8729-1bdff77ff6d6
ms.openlocfilehash: 7dc38acbe91e03f579414294da07bff5cc53cc4c
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="discovery-binding-element-sample"></a>发现绑定元素示例
本示例演示如何使用发现客户端绑定元素发现服务。 开发人员使用此功能可以向其现有客户端通道堆栈添加发现客户端通道，从而使编程模型非常直观。 当关联通道打开时，会使用发现解析服务地址。 本示例包含以下项目：  
  
-   **CalculatorService**： 的可检测到[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]服务。  
  
-   **CalculatorClient**: A[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]使用 discovery 客户端通道搜索并调用 CalculatorService 的客户端应用程序。  
  
-   **DynamicCalculatorClient**: A[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]使用动态终结点搜索并调用 CalculatorService 的客户端应用程序。  
  
> [!IMPORTANT]
>  您的计算机上可能已安装这些示例。 在继续操作之前，请先检查以下（默认）目录：  
>   
>  `<InstallDrive>:\WF_WCF_Samples`  
>   
>  如果此目录不存在，请转到[Windows Communication Foundation (WCF) 和针对.NET Framework 4 的 Windows Workflow Foundation (WF) 示例](http://go.microsoft.com/fwlink/?LinkId=150780)下载所有 Windows Communication Foundation (WCF) 和[!INCLUDE[wf1](../../../../includes/wf1-md.md)]示例。 此示例位于以下目录：  
>   
>  `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Discovery\DiscoveryBindingElement`  
  
## <a name="calculatorservice"></a>CalculatorService  
 此项目包含一个实现 `ICalculatorService` 协定的简单计算器服务。  
  
 下面的 App.config 文件用于在服务行为和发现终结点中添加 `<serviceDiscovery>` 行为。  
  
```xml  
<system.serviceModel>  
    <services>  
      <service behaviorConfiguration="CalculatorBehavior" name="Microsoft.Samples.Discovery.CalculatorService">  
        <endpoint name="udpDiscoveryEpt" kind="udpDiscoveryEndpoint" />  
      </service>  
    </services>  
    <behaviors>  
      <!--Enable discovery through configuration.-->  
      <serviceBehaviors>  
        <behavior name="CalculatorBehavior">  
          <serviceDiscovery>  
          </serviceDiscovery>  
        </behavior>  
      </serviceBehaviors>  
    </behaviors>  
  </system.serviceModel>  
```  
  
 这使得服务及其终结点可发现。 CalculatorService 是使用 NetTcpBinding 绑定添加一个终结点的自承载服务。 它还向终结点添加 `EndpointDiscoveryBehavior` 并指定范围，如下面的节点中所示。  
  
```  
// Add a NET.TCP endpoint and add a scope to that endpoint.  
ServiceEndpoint netTcpEndpoint = serviceHost.AddServiceEndpoint(typeof(ICalculatorService), new NetTcpBinding(), netTcpAddress);  
EndpointDiscoveryBehavior netTctEndpointBehavior = new EndpointDiscoveryBehavior();  
netTctEndpointBehavior.Scopes.Add(new Uri("ldap:///ou=engineering,o=exampleorg,c=us"));  
netTcpEndpoint.Behaviors.Add(netTctEndpointBehavior);  
serviceHost.Open();  
```  
  
## <a name="calculatorclient"></a>CalculatorClient  
 此项目包含一个向 CalculatorService 发送消息的客户端实现。 此程序使用 `CreateCustomBindingWithDiscoveryElement()` 方法创建一个使用 Discovery 客户端通道的自定义绑定。  
  
```  
static CustomBinding CreateCustomBindingWithDiscoveryElement()  
 {  
      DiscoveryClientBindingElement discoveryBindingElement = new DiscoveryClientBindingElement();  
  
            // Provide the search criteria and the endpoint over which the probe is sent  
            discoveryBindingElement.FindCriteria = new FindCriteria(typeof(ICalculatorService));  
            discoveryBindingElement.DiscoveryEndpointProvider = new UdpDiscoveryEndpointProvider();  
  
            CustomBinding customBinding = new CustomBinding(new NetTcpBinding());  
            // Insert DiscoveryClientBindingElement at the top of the BindingElement stack.  
            // An exception is thrown if this binding element is not at the top  
            customBinding.Elements.Insert(0, discoveryBindingElement);  
  
            return customBinding; }  
```  
  
 <xref:System.ServiceModel.Discovery.DiscoveryClientBindingElement> 实例化后，开发人员指定搜索服务时要使用的条件。 在本例中，发现查找条件是 `ICalculatorService` 类型。 此外，开发人员还指定一个 <xref:System.ServiceModel.Discovery.DiscoveryEndpointProvider>，它返回指定要在何处查找服务的 <xref:System.ServiceModel.Discovery.DiscoveryEndpoint>。 <xref:System.ServiceModel.Discovery.DiscoveryEndpointProvider> 返回新的 <xref:System.ServiceModel.Discovery.DiscoveryEndpoint> 实例。 有关详细信息，请参阅[通过 Discovery 客户端通道使用自定义绑定](../../../../docs/framework/wcf/feature-details/using-a-custom-binding-with-the-discovery-client-channel.md)。  
  
```  
// Extend DiscoveryEndpointProvider class to change the default DiscoveryEndpoint  
    // to the DiscoveryClientBindingElement. The Discovery ClientChannel   
    // uses this endpoint to send Probe message.  
    public class UdpDiscoveryEndpointProvider : DiscoveryEndpointProvider  
    {  
        public override DiscoveryEndpoint GetDiscoveryEndpoint()  
        {  
            return new UdpDiscoveryEndpoint(DiscoveryVersion.WSDiscoveryApril2005);  
        }  
    }  
```  
  
 在本例中，客户端使用 Discovery 协议定义的 UDP 多播机制在本地子网上搜索服务。 方法的其余部分创建自定义绑定并将 Discovery 绑定元素插入堆栈顶部。  
  
> [!NOTE]
>  <xref:System.ServiceModel.Discovery.DiscoveryClientBindingElement> 必须放置在绑定堆栈顶部。 <xref:System.ServiceModel.Channels.BindingElement> 之上的任何 <xref:System.ServiceModel.Discovery.DiscoveryClientBindingElement> 都必须确保其创建的通道工厂或通道不使用 `EndpointAddress` 或 `Via` 属性，因为实际地址只能在 Discovery 客户端通道上发现。  
  
 接下来，可以通过传入此自定义绑定和终结点地址来实例化 `CalculatorClient`。  
  
```  
CalculatorServiceClient client = new CalculatorServiceClient(CreateCustomBindingWithDiscoveryElement(), DiscoveryClientBindingElement.DiscoveryEndpointAddress);  
```  
  
 在使用发现客户端通道时，将传入先前指定的恒定终结点地址。 现在，在运行时，发现客户端通道查找通过查找条件指定的服务，并与其连接。 若要使服务和客户端建立连接，它们必须具有相同的基础绑定堆栈。  
  
#### <a name="to-use-this-sample"></a>使用此示例  
  
1.  在 [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)] 中打开解决方案。  
  
2.  生成解决方案。  
  
3.  运行服务应用程序和每个客户端应用程序。  
  
4.  观察客户端是否能够在不知道服务地址的情况下找到服务。  
  
## <a name="see-also"></a>请参阅
