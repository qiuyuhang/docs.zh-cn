---
title: 配置应用程序
ms.date: 03/30/2017
ms.assetid: a2f995b0-669d-4721-b00f-4561ec7eb6a4
ms.openlocfilehash: 7dfd662fafa636e0fa97f118217ad1786d5aa444
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="configuring-your-application"></a>配置应用程序
Windows Communication Foundation (WCF) 使用.NET 配置系统，并允许你在计算机和应用程序范围配置服务。  
  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 定义的配置设置位于 `<system.serviceModel>` 节组中。 有关如何配置详细信息[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]服务，请参阅以下主题：  
  
-   [配置服务](../../../../docs/framework/wcf/configuring-services.md)  
  
-   [\<system.serviceModel>](../../../../docs/framework/configure-apps/file-schema/wcf/system-servicemodel.md)  
  
 应用程序定义的配置设置是在 `<appSettings>` 节组中定义的。 有关.NET 配置文件中的应用程序设置的详细信息，请参阅[ \<appSettings >](http://go.microsoft.com/fwlink/?LinkId=95159)。  
  
## <a name="using-the-configuration-editor"></a>使用配置编辑器  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)][配置编辑器工具 (SvcConfigEditor.exe)](../../../../docs/framework/wcf/configuration-editor-tool-svcconfigeditor-exe.md)允许管理员和开发人员创建和修改配置设置[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]服务使用图形用户界面。 利用此工具，您无需直接编辑 XML 配置文件就可管理 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 绑定、行为、服务和诊断的设置。  
  
## <a name="editing-configuration-files-in-visual-studio"></a>在 Visual Studio 中编辑配置文件  
 若要编辑的配置文件[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]服务 Visual Studio 中的项目，请右键单击在**解决方案资源管理器**选择**编辑 WCF 配置**上下文菜单项。 这将启动[配置编辑器工具 (SvcConfigEditor.exe)](../../../../docs/framework/wcf/configuration-editor-tool-svcconfigeditor-exe.md)。  
  
> [!NOTE]
>  如果编辑的配置文件[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]Visual Studio 中，右键单击该中的 Web 服务项目**解决方案资源管理器**，请注意，**编辑 WCF 配置**未提供的上下文菜单项。 解决此问题，请单击**工具**菜单上，选择**WCF 服务配置编辑器**。 之后，你可以右键单击配置文件并使用**编辑 WCF 配置**上下文菜单项。  
  
## <a name="see-also"></a>请参阅  
 [配置编辑器工具 (SvcConfigEditor.exe)](../../../../docs/framework/wcf/configuration-editor-tool-svcconfigeditor-exe.md)  
 [配置服务](../../../../docs/framework/wcf/configuring-services.md)  
 [\<system.serviceModel>](../../../../docs/framework/configure-apps/file-schema/wcf/system-servicemodel.md)
