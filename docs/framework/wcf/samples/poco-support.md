---
title: POCO 支持
ms.custom: ''
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 3846ca73-2819-4ca2-8367-dc739dde5a5b
caps.latest.revision: 11
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload:
- dotnet
ms.openlocfilehash: 9c67b39c8d3c48281eb0ec9c360de7eaff1cfad6
ms.sourcegitcommit: 94d33cadc5ff81d2ac389bf5f26422c227832052
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/30/2018
---
# <a name="poco-support"></a>POCO 支持
此示例演示对未标记的类型的序列化支持，未标记的类型是指尚未应用序列化属性的类型，有时称作“简单传统 CLR 对象 (POCO)”类型。 <xref:System.Runtime.Serialization.DataContractSerializer> 为所有具有默认构造函数的公共未标记类型推断一个数据协定。 数据协定允许您在服务中传入和传出结构化数据。 有关未标记的类型的详细信息，请参阅[可序列化类型](../../../../docs/framework/wcf/feature-details/serializable-types.md)。  
  
 此示例基于[入门](../../../../docs/framework/wcf/samples/getting-started-sample.md)，但使用而不是基元数值类型的复数。 它也是类似于[基本数据协定](../../../../docs/framework/wcf/samples/basic-data-contract.md)示例，只不过<xref:System.Runtime.Serialization.DataContractAttribute>和<xref:System.Runtime.Serialization.DataMemberAttribute>不使用属性。  
  
 服务是由 Internet 信息服务 (IIS) 承载的，客户端是一个控制台应用程序 (.exe)。  
  
> [!NOTE]
>  本主题的最后介绍了此示例的设置过程和生成说明。  
  
 `ComplexNumber` 类在 `ServiceContract` 中使用。 `ComplexNumber` 类型没有 <xref:System.Runtime.Serialization.DataContractAttribute> 和 <xref:System.Runtime.Serialization.DataMemberAttribute> 属性，如下面的示例代码所示。 默认情况下，所有公共属性和字段均被序列化。  
  
```  
public class ComplexNumber  
{  
    public double Real;  
    public double Imaginary;  
    public ComplexNumber()  
    {  
        Real = double.MinValue;  
        Imaginary = double.MinValue;  
    }  
    public ComplexNumber(double real, double imaginary)  
    {  
        this.Real = real;  
        this.Imaginary = imaginary;  
    }  
}  
```  
  
### <a name="to-set-up-build-and-run-the-sample"></a>设置、生成和运行示例  
  
1.  确保已执行[的 Windows Communication Foundation 示例的一次性安装过程](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md)。  
  
2.  若要生成 C# 或 Visual Basic .NET 版本的解决方案，请按照 [Building the Windows Communication Foundation Samples](../../../../docs/framework/wcf/samples/building-the-samples.md)中的说明进行操作。  
  
3.  若要在单或跨计算机配置上运行示例，请按照中的说明[运行 Windows Communication Foundation 示例](../../../../docs/framework/wcf/samples/running-the-samples.md)。  
  
> [!IMPORTANT]
>  您的计算机上可能已安装这些示例。 在继续操作之前，请先检查以下（默认）目录：  
>   
>  `<InstallDrive>:\WF_WCF_Samples`  
>   
>  如果此目录不存在，请访问 [针对 .NET Framework 4 的 Windows Communication Foundation (WCF) 和 Windows Workflow Foundation (WF) 示例](http://go.microsoft.com/fwlink/?LinkId=150780) 以下载所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 示例。 此示例位于以下目录：  
>   
>  `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Contract\Data\POCO`  
  
## <a name="see-also"></a>请参阅  
 <xref:System.Runtime.Serialization.IgnoreDataMemberAttribute>  
 [可序列化类型](../../../../docs/framework/wcf/feature-details/serializable-types.md)
