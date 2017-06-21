---
title: "如何：使用 MetadataResolver 动态获取绑定元数据 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 56ffcb99-fff0-4479-aca0-e3909009f605
caps.latest.revision: 12
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 12
---
# 如何：使用 MetadataResolver 动态获取绑定元数据
本主题演示如何使用 <xref:System.ServiceModel.Description.MetadataResolver> 类来动态获取绑定元数据。  
  
### 动态获取绑定元数据  
  
1.  使用元数据终结点的地址创建一个 <xref:System.ServiceModel.EndpointAddress> 对象。  
  
    ```  
    EndpointAddress metaAddress  
      = new EndpointAddress(new   Uri("http://localhost:8080/SampleService/mex"));  
    ```  
  
2.  调用 <xref:System.ServiceModel.Description.MetadataResolver.Resolve%28System.Type%2CSystem.ServiceModel.EndpointAddress%29>，它传入服务类型和元数据终结点地址。这将返回实现了指定协定的终结点的集合。仅从元数据导入绑定信息；不导入协定信息。改用所提供的协定。  
  
    ```  
    ServiceEndpointCollection endpoints = MetadataResolver.Resolve(typeof(SampleServiceClient),metaAddress);  
    ```  
  
3.  然后，可以遍历该服务终结点集合，以提取所需的绑定信息。下面的代码遍历终结点，创建一个服务客户端对象（该对象传入与当前终结点关联的绑定和地址），然后调用该服务上的一个方法。  
  
    ```  
    foreach (ServiceEndpoint point in endpoints)  
    {  
       if (point != null)  
       {  
          // Create a new wcfClient using retrieved endpoints.  
          using (wcfClient = new SampleServiceClient(point.Binding, point.Address))  
          {  
             Console.WriteLine(  
               wcfClient.SampleMethod("Client used the "  
               + point.Address.ToString() + " address."));  
          }  
      }  
    }  
    ```  
  
## 请参阅  
 [元数据](../../../../docs/framework/wcf/feature-details/metadata.md)