---
title: 动态启用分析跟踪
ms.date: 03/30/2017
ms.assetid: 58b63cfc-307a-427d-b69d-9917ff9f44ac
ms.openlocfilehash: 46dfba2cb148009ddfd0bbd40e3b7202d774e0b7
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="dynamically-enabling-analytic-tracing"></a>动态启用分析跟踪
通过 Windows 操作系统附带的工具，可以使用 Windows 事件跟踪 (ETW) 动态启用或禁用跟踪。 所有[!INCLUDE[netfx_current_long](../../../../../includes/netfx-current-long-md.md)]Windows Communication Foundation (WCF) 服务，分析跟踪可以启用和禁用动态而无需修改应用程序的 Web.config 文件或重新启动服务。 这样，发出跟踪事件的应用程序就可以保持原样。  
  
 可以采用类似方式配置[!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] 跟踪选项。 例如，可以将严重性级别从 **Error** 更改为 **Information** 而不影响应用程序。 可以使用以下工具来实现此功能：  
  
-   **Logman** – 一个命令行工具，用于配置、控制和查询跟踪数据。 有关详细信息，请参阅[Logman 创建跟踪](http://go.microsoft.com/fwlink/?LinkId=165426)和[Logman 更新跟踪](http://go.microsoft.com/fwlink/?LinkId=165427)。  
  
-   **EventViewer** - Windows 图形管理工具，用于查看跟踪的结果。 有关详细信息，请参阅[WCF 服务和 Windows 事件跟踪](../../../../../docs/framework/wcf/samples/wcf-services-and-event-tracing-for-windows.md)和[事件查看器](http://go.microsoft.com/fwlink/?LinkId=165428)。  
  
-   **Perfmon** – Windows 图形管理工具，它使用计数器监视跟踪计数器以及跟踪对性能的影响。 有关详细信息，请参阅[数据收集器设置手动创建](http://go.microsoft.com/fwlink/?LinkId=165429)。  
  
### <a name="keywords"></a>关键字  
 使用 <xref:System.ServiceModel.Activation.Configuration.ServiceModelActivationSectionGroup.Diagnostics%2A> 类时，通常按严重性级别（如 Error、Warning 和 Information）筛选 .NET Framework 跟踪消息。 ETW 支持严重性级别概念，但引入了使用关键字的新型灵活筛选器机制。 关键字为任意文本值，用于使跟踪事件提供有关事件含义的附加上下文。  
  
 对于 [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] 分析跟踪，每个跟踪事件都有两种关键字。 首先，每个事件包含一个或多个方案关键字。 这类关键字表示此事件将支持的各方案。 有三个方案关键字，每一个方案关键字均设计用于特定用途，如下表所示。 可以动态更改使用关键字进行的筛选而不会干扰 [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] 服务。 这意味着您可以动态更改当前跟踪方案以及所收集的跟踪信息量。 例如，您可以将 `HealthMonitoring` 更改为 `Troubleshooting` ，并增加跟踪事件粒度。  
  
|关键字|描述|  
|-------------|-----------------|  
|`HealthMonitoring`|非常轻量、程度最低的跟踪，用于监视服务活动。|  
|`EndToEndMonitoring`|用于支持消息流跟踪的事件。|  
|`Troubleshooting`|围绕 [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)]扩展点的粒度更细的事件。|  
  
 第二组关键字定义 [!INCLUDE[dnprdnshort](../../../../../includes/dnprdnshort-md.md)] 的哪个组件发出了事件。  
  
|关键字|描述|  
|-------------|-----------------|  
|`UserEvents`|由用户代码而非 [!INCLUDE[dnprdnshort](../../../../../includes/dnprdnshort-md.md)]发出的事件。|  
|`ServiceModel`|由 [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] 运行时发出的事件。|  
|`ServiceHost`|由服务主机发出的事件。|  
|`WCFMessageLogging`|[!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] 消息日志记录事件。|  
  
## <a name="see-also"></a>请参阅  
 [WCF Services and Event Tracing for Windows](../../../../../docs/framework/wcf/samples/wcf-services-and-event-tracing-for-windows.md)
