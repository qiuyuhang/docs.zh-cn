---
title: 配置编辑器工具 (SvcConfigEditor.exe)
ms.date: 03/30/2017
helpviewer_keywords:
- configuration files, creating
- configuration files
- Configuration file
- configuration file schema
ms.assetid: 2db21a57-5f64-426f-89df-fb0dc2d2def5
ms.openlocfilehash: ab6e3a99f951d2977a079f49e4aa3eff250ee8d5
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="configuration-editor-tool-svcconfigeditorexe"></a>配置编辑器工具 (SvcConfigEditor.exe)
Windows Communication Foundation (WCF) 服务配置编辑器 (SvcConfigEditor.exe) 允许管理员和开发人员创建和修改配置设置[!INCLUDE[indigo2](../../../includes/indigo2-md.md)]服务使用图形用户界面。 利用此工具，您不必直接编辑 XML 配置文件就可管理 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 绑定、行为、服务和诊断的设置。  
  
 在 C:\Program Files\Microsoft SDKs\Windows\v6.0\Bin 文件夹中可以找到服务配置编辑器。  
  
## <a name="the-wcf-configuration-editor"></a>WCF 配置编辑器  
 服务配置编辑器附带了一个向导，该向导可引导您完成配置 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 服务或客户端的所有步骤。 强烈建议您使用向导，而不是直接使用编辑器。  
  
 如果已经有一些符合标准 System.Configuration 架构的配置文件，可通过用户界面管理绑定、行为、服务和诊断的特定设置。 使用服务配置编辑器，可以管理现有 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 配置文件的设置，以及可执行文件、COM+ 服务和 Web 承载的服务的设置。 用服务配置编辑器打开 Web 承载的服务时，会同时显示服务自己的配置节和从上级节点继承的配置节。  
  
 由于 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 配置设置位于配置文件的 `<system.serviceModel>` 节中，编辑器只会对此元素的内容进行操作，而不会访问同一文件中的其他元素。 可以直接定位到现有配置文件，也可以选择包含服务、虚拟目录或 COM+ 服务的程序集。 编辑器将为该特定服务加载配置文件，并允许用户添加新元素或编辑嵌套在配置文件的 `<system.serviceModel>` 节中的现有元素。  
  
 编辑器支持 IntelliSense，并强制遵从架构要求。 可以保证生成的输出符合配置文件的架构，并具有在语法上正确的数据值。 但是，编辑器不保证配置文件在语义上是有效的。 换句话说，编辑器不保证配置文件可与它配置的服务协同工作。  
  
> [!CAUTION]
>  一旦您修改了某个配置元素后，编辑器将无法从配置文件中清除该元素。 例如，如果使用编辑器将终结点名称设置为非空字符串并加以保存，则配置文件会具有以下内容，如下面的示例所示。  
>   
>  `<endpoint binding="basicHttpBinding" name="somename" />`  
>   
>  如果尝试通过将名称设置为空字符串来移除名称并保存文件，则配置文件仍会包含 `name` 特性，如下面的示例所示。  
>   
>  `<endpoint binding="basicHttpBinding" name="" />`  
>   
>  若要清除该属性，您必须使用另一个文本编辑器手动编辑该元素。  
>   
>  在使用 `issueToken` 终结点行为的 `clientCredential` 元素时，应要特别小心此问题。 特别是，其 `address` 子元素的 `localIssuer` 特性一定不能为空字符串。 如果使用配置编辑器修改了 `address` 特性并且想要完全移除该特性，您应使用除该编辑器之外的其他工具来进行操作。 否则，该特性会包含空字符串，并且应用程序会引发异常。  
  
## <a name="using-the-configuration-editor"></a>使用配置编辑器  
 可在以下 Windows SDK 安装位置中找到服务配置编辑器：  
  
 C:\Program Files\Microsoft SDKs\Windows\v6.0\Bin\SvcConfigEditor.exe  
  
 启动服务配置编辑器后，你可以使用**文件 / 打开**菜单浏览服务或你想要管理的程序集。 可以直接打开配置文件、浏览 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] /COM+ 服务，以及打开 Web 承载的服务的配置文件。  
  
 服务配置编辑器的用户界面分成以下几个区域：  
  
-   树视图窗格，在左侧以树状结构显示配置元素。 右击节点可在树中执行操作。  
  
-   任务窗格，在窗口的左下方显示了当前元素的常见任务  
  
-   详细信息窗格，在右侧显示了树视图中所选配置节点的详细设置。  
  
### <a name="opening-a-configuration-file"></a>打开配置文件  
  
1.  启动服务配置编辑器，通过使用命令窗口导航到你[!INCLUDE[indigo2](../../../includes/indigo2-md.md)]安装位置，然后键入`SvcConfigEditor.exe`。  
  
2.  从**文件**菜单上，选择**打开**单击你想要管理的文件的类型。  
  
3.  在**打开**对话框框中，导航到你想要管理并双击它的特定文件。  
  
 查看器自动跟随配置合并路径，并创建合并配置的视图。 例如，非宿主服务的实际配置是 Machine.config 和 App.config 的组合。任何更改都将应用于 SvcConfigEditor 中当前打开的文件。 如果要编辑配置合并路径中的特定文件，应直接将其打开。  
  
> [!NOTE]
>  如果在编辑器外部修改了后者，配置编辑器将重新加载当前打开的配置文件。 发生这种情况时，未在编辑器内永久保存的所有更改都将丢失。 如果一直发生重新加载情况，最可能的原因是某项服务（例如，在后台运行的防病毒软件）在不断地访问配置文件。 若要解决此问题，请确保配置编辑器是在文件打开时唯一能够访问该文件的进程。  
  
### <a name="services"></a>服务  
 **服务**节点显示所有当前分配的配置文件中的服务。 每个树中的子节点对应的子元素 <`services`> 配置文件中的元素。  
  
 当你单击**服务**节点，你可以查看或执行任务在服务上的摘要页中**详细信息**窗格。  
  
#### <a name="creating-a-new-service-configuration"></a>创建新的服务配置  
 可按下列方法创建新的服务配置：  
  
-   使用向导： 单击链接**创建新的服务...** 上的任务窗格或摘要页以启动向导。 你还可以执行在**文件**菜单->**添加新项**。  
  
-   手动创建： 可右击**服务**节点，然后选择**新服务**。  
  
#### <a name="creating-a-new-service-endpoint-configuration"></a>创建新的服务终结点配置  
 可按下列方法创建新的服务终结点配置：  
  
-   使用向导创建： 单击链接**创建新的服务终结点...** 上的任务窗格或摘要页以启动向导。 你还可以执行在**文件**菜单->**添加新项**。  
  
-   手动创建： 一旦创建了服务，你可以右键单击**终结点**节点，然后选择"**新建服务终结点**"。  
  
#### <a name="editing-a-service-configuration"></a>编辑服务配置  
  
1.  单击**服务**节点。  
  
2.  在属性网格中编辑设置。  
  
#### <a name="editing-a-service-endpoint-configuration"></a>编辑服务终结点配置  
  
1.  单击**服务终结点**节点。  
  
2.  在属性网格中编辑设置。  
  
#### <a name="adding-a-base-address"></a>添加基址  
  
1.  单击**主机**节点。  
  
2.  单击**新...** 按钮**基址**部分。  
  
3.  在对话框中键入基址 URI。  
  
4.  单击 **“确定”**。  
  
> [!NOTE]
>  不能编辑的值[ \<Baseaddressprefixfilter >](../../../docs/framework/configure-apps/file-schema/wcf/baseaddressprefixfilters.md)内此工具。 若要添加或修改此元素，应使用文本编辑器或 Visual Studio。  
  
### <a name="client"></a>客户端  
 **客户端**节点显示所有客户端终结点的配置文件中。 在树中的每个子节点对应的子元素 <`client`> 配置文件中的元素。  
  
 当你单击**客户端**节点，你可以查看或客户端上执行任务**摘要页**中**详细信息窗格**。  
  
#### <a name="creating-a-new-client-endpoint-configuration"></a>创建新的客户端终结点配置  
 可按下列方法创建新的客户端终结点配置：  
  
-   向导创建： 单击链接**创建新的客户端...** 上**任务窗格**窗口的左下方或**摘要页**以启动向导。 你还可以执行在**文件**菜单->**添加新项**。 该向导会提示您指向从中生成客户端配置的服务配置的位置。 然后，您可以选择要连接的服务终结点。  
  
-   手动创建： 右击**终结点**节点下的**客户端**，然后选择**新客户端终结点**。  
  
#### <a name="editing-a-client-endpoint-configuration"></a>编辑客户端终结点配置  
  
1.  单击**客户端终结点**节点。  
  
2.  在属性网格中编辑设置。  
  
### <a name="standard-endpoint"></a>标准终结点  
 标准终结点是一种专门的终结点，其地址、协定和绑定中的一个或多个方面已设置为默认值。  
  
 此类配置设置存储在**标准终结点**节点。 **标准终结点**节点可显示在配置文件中的所有标准终结点设置。 在树中的每个子节点对应于中的子元素`<standardEndpoints>`配置文件中的元素。  
  
 当你单击**标准终结点**节点，您可以查看或执行任务的标准终结点上**摘要页**中**详细信息窗格**。  
  
#### <a name="creating-a-new-standard-endpoint-configuration"></a>创建新的标准终结点配置  
 可按下列方法创建新的标准终结点配置：  
  
-   右键单击**标准终结点**节点，然后选择**新建标准终结点配置...** 在对话框中选择绑定类型，然后单击**确定**。  
  
-   选择**标准终结点**节点，然后单击**新建标准终结点配置...** 在**任务窗格**窗口的左下方。  
  
 **创建新的标准终结点**对话框中显示，并列出所有已注册的标准终结点类型。  
  
#### <a name="viewing-and-editing-a-standard-endpoint-configuration"></a>查看和编辑标准终结点配置  
 可按下列方法打开标准终结点配置以供查看和编辑：  
  
-   单击以展开**标准终结点**节点并单击相应的终结点子节点。  
  
-   单击**标准终结点**节点，然后单击详细信息窗格上的相应终结点。  
  
 终结点的特性将显示在右侧窗格中以供编辑。  
  
#### <a name="deleting-a-standard-endpoint-configuration"></a>删除标准终结点配置  
 可按下列方法删除标准终结点配置：  
  
-   单击以展开**标准终结点**节点并右击相应的终结点子节点。 使用上下文命令**删除标准终结点配置**要删除终结点。  
  
-   单击**标准终结点**节点。 在**任务**窗格中，单击**删除标准终结点配置**。  
  
 如果标准终结点正被使用，则在尝试删除时将显示一条警报消息：**“该标准终结点正被使用。如果现在删除，请确保删除其他配置部分中(例如，从服务终结点或客户端终结点中)对该标准终结点的所有引用。否则，配置将无效，并且下次将无法打开。是否确实要删除的标准终结点？"**  
  
### <a name="binding"></a>绑定  
 绑定配置用于配置终结点上的绑定。 此类配置设置存储在**绑定**节点。 终结点按名称引用绑定配置，并且多个终结点可引用同一个绑定配置。  
  
 **绑定**节点可显示的所有绑定设置中配置文件。 在树中的每个子节点对应于中的子元素 <`bindings`> 配置文件中的元素。  
  
 当你单击**绑定**节点，您可以查看或执行任务，在绑定上**摘要页**中**详细信息窗格**。  
  
#### <a name="creating-a-new-binding-configuration"></a>创建新的绑定配置  
 可按下列方法创建新的绑定配置。  
  
-   右键单击**绑定**节点，然后选择**新建绑定配置**... 在对话框中选择绑定类型，然后单击**确定**。  
  
-   选择**绑定**节点，然后单击**新建绑定配置**... 在**任务窗格**窗口的左下方。  
  
-   在服务或客户端摘要页中，单击**单击此处进行创建**中**绑定配置**字段创建相应的终结点的绑定配置。  
  
#### <a name="adding-binding-element-extensions-to-a-custom-binding"></a>向自定义绑定添加绑定元素扩展  
  
1.  选择要向其添加扩展元素的绑定。  
  
2.  单击 **添加**。  
  
3.  从可用扩展列表中，选择要添加的绑定元素扩展。 按住 Ctrl 键的同时进行选择可选择多项。  
  
4.  单击 **添加**。  
  
#### <a name="adjusting-the-extension-position-in-a-custom-binding"></a>调整自定义绑定中的扩展位置  
 自定义绑定是形成堆栈的一系列绑定元素。 堆栈中的每个绑定元素都有其自己的配置设置。 绑定元素扩展在自定义绑定中的顺序指示它们在堆栈中的位置。 堆栈顶部的元素首先得到应用。 若要更改顺序：  
  
1.  选择自定义绑定节点。  
  
2.  选择中的一个绑定扩展元素**绑定元素扩展位置**部分。  
  
3.  使用**向上**或**下**要更改所选元素的位置的列表左侧的按钮。  
  
#### <a name="editing-the-configuration-of-binding-element-extensions-in-a-custom-binding"></a>编辑自定义绑定中的绑定元素扩展的配置  
  
1.  选择树中的绑定节点。  
  
2.  选择包含要编辑的元素的自定义绑定。  
  
3.  选择要编辑的绑定元素扩展。 该元素的设置将出现在右窗格中，可在其中编辑这些设置。  
  
### <a name="diagnostics"></a>诊断  
 **诊断**节点可显示在配置文件中的所有诊断设置。 它使您能够开关性能计数器、启用或禁用 Windows Management Instrumentation (WMI)、配置 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 跟踪，以及配置 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 消息日志记录。 中的设置**诊断**节点对应于 <`system.diagnostics`> 部分中，和`<diagnostics>`主题中`<system.serviceModel>`配置文件中。  
  
 当你单击**诊断**节点，您可以查看或执行诊断任务**摘要页**中**详细信息窗格**。  
  
#### <a name="configuring-performance-counters-and-wmi"></a>配置性能计数器和 WMI  
  
1.  单击**诊断**节点。  
  
2.  单击**切换性能计数器**。 性能计数器有三种状态：Off（默认）、ServiceOnly 和 All。 单击链接可在这三种状态之间切换设置。  
  
#### <a name="configuring-wmi-provider"></a>配置 WMI 提供程序  
  
1.  单击**诊断**节点。  
  
2.  若要启用 WMI 提供程序，请单击**启用 WMI 提供程序**链接。  
  
#### <a name="enabling-wcf-tracing"></a>启用 WCF 跟踪  
 可创建具有标准属性的 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 跟踪文件，或者设置自定义的跟踪文件。  
  
1.  单击**诊断**节点。  
  
2.  单击**启用跟踪**。  
  
3.  单击**跟踪级别**链接调整跟踪级别。 有六种跟踪级别：“禁用”、“严重”、“错误”、“警告”、“信息”和“详细”。 **活动跟踪**和**传播活动**选项使您能使用[!INCLUDE[indigo2](../../../includes/indigo2-md.md)]活动跟踪功能。  
  
4.  单击跟踪侦听器名称指定跟踪文件和选项。  
  
#### <a name="enabling-wcf-logging"></a>启用 WCF 日志记录  
 可创建具有标准属性的 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 跟踪文件，或者设置自定义的跟踪文件。  
  
1.  单击**诊断**节点。  
  
2.  单击**启用消息日志记录**。  
  
3.  单击**日志级别**链接调整日志级别。 有 3 种日志级别：“格式错误”、“服务”和“传输”。  
  
4.  单击侦听器名称指定日志文件和选项。  
  
> [!NOTE]
>  如果你想要关闭你的应用程序时自动刷新，启用的跟踪和消息日志**自动刷新**选项。  
  
 **诊断****摘要页**使您能够完成配置诊断中的最常见任务。 但是，如果你想要手动编辑侦听器和源设置，你必须展开**诊断**中的节点，然后编辑设置**消息日志记录**，**侦听器**和**源**节点。  
  
#### <a name="enabling-wcf-custom-tracing-or-message-logging"></a>启用 WCF 自定义跟踪或消息日志记录  
  
1.  单击**诊断**节点，并将其展开。  
  
2.  右键单击**侦听器**节点，然后选择**新侦听器**。  
  
3.  中的跟踪文件名称中的类型**InitData**字段。 你可以单击"..."按钮以浏览到的路径。  
  
4.  单击**TypeName**行显示一个"..."按钮。 单击此按钮可打开**跟踪侦听器类型浏览器**，可以用于查找已安装的预先配置的跟踪侦听器。  
  
5.  请注意**源**部分。 单击**添加**中此部分以带有下拉列表菜单中打开一个对话框，其中列出了可用的跟踪源。 选择一个跟踪源，然后单击**确定**。  
  
6.  若要编辑消息日志记录设置，请单击**消息日志记录**节点。 可在属性网格中编辑这些设置。  
  
### <a name="advanced"></a>高级  
  
#### <a name="behaviors"></a>行为  
 **行为**节点显示当前配置文件中定义的行为。  
  
 行为配置用于配置终结点和服务的行为。 此类配置设置存储在**高级**节点下的**服务行为**和**终结点行为**。 服务行为由服务使用；而终结点行为则由终结点使用。  
  
 行为是形成堆栈的一系列扩展元素。 堆栈顶部的元素首先得到应用。 每个扩展元素可有其自己的配置。  
  
##### <a name="creating-a-new-behavior-configuration"></a>创建新的行为配置  
 可通过以下两种方法创建新的行为配置。  
  
-   右键单击其中一个行为节点，然后选择"**新建行为配置...**  
  
-   选择一个行为节点，然后单击**新建行为配置**... 在**任务窗格**窗口的左下方。  
  
##### <a name="adding-behavior-element-extensions-to-a-behavior"></a>向行为中添加行为元素扩展  
  
1.  选择一个行为节点。  
  
2.  选择要编辑的行为。  
  
3.  单击 **添加**。  
  
4.  从可用扩展列表中，选择要添加的行为元素扩展。  
  
5.  单击 **添加**。  
  
##### <a name="adjusting-the-extension-position-in-a-behavior"></a>调整行为中的扩展位置  
 行为是形成堆栈的元素集合。 堆栈中的每个元素都有其自己的配置。 行为元素扩展在行为中的顺序指示它们在堆栈中的位置。 堆栈顶部的元素首先得到应用。 若要更改顺序：  
  
1.  选择一个行为节点。  
  
2.  选择要编辑的行为。  
  
3.  选择中的行为扩展元素**行为元素扩展位置**部分。  
  
4.  使用**向上**或**下**要更改所选元素的位置的列表左侧的按钮。  
  
##### <a name="editing-the-configuration-of-behavior-element-extensions"></a>编辑行为元素扩展的配置  
  
1.  选择树中的一个行为节点。  
  
2.  选择包含要编辑的元素的行为。  
  
3.  选择要编辑的行为元素扩展。 该元素的设置将出现在右窗格中，可在其中编辑这些设置。  
  
#### <a name="protocolmapping"></a>ProtocolMapping  
 使用本节，可以通过协议地址方案和可能的绑定之间已定义的映射，来设置不同协议（如 http、tcp、MSMQ 或 net.pipe）的默认绑定类型。 还可以添加对其他协议的新映射。  
  
#### <a name="extensions"></a>扩展  
 可注册新的绑定扩展、绑定元素扩展、标准终结点扩展和行为扩展以在 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 配置中使用。 扩展是名称/类型对。 名称定义扩展在配置中的名称，而类型则实现该扩展。 有四种类型的扩展：  
  
-   绑定扩展定义整个绑定类型。 示例：`basicHttpBinding`。  
  
-   绑定元素扩展定义绑定的元素。 示例：`textMessageEncoding`。  
  
-   标准终结点扩展定义整个标准终结点。 示例：`discoveryEndpoint`。  
  
-   行为元素扩展定义行为的元素。 示例：`clientVia`。  
  
 可像使用同类型的任何其他 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 组件一样使用已在配置中注册的扩展。  
  
##### <a name="adding-a-new-extension"></a>添加新扩展  
 选择高级节点中的某个扩展节点：  
  
1.  单击“新建” 。  
  
2.  输入名称和类型。  
  
3.  单击 **“确定”**。  
  
4.  扩展现在出现在编辑器中的适当位置。 例如，如果添加了行为元素扩展，它将出现在可用扩展的列表中。  
  
#### <a name="hosting-environment"></a>宿主环境  
 本节介绍如何为服务主机环境定义实例化设置。  
  
### <a name="creating-a-configuration-file-using-the-wizard"></a>使用向导创建配置文件  
 创建新配置文件的一种方法是使用“新建服务元素向导”。 该向导查找计算机上已安装的服务类型以及其他与 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 兼容的元素（包括 COM+ 和 Web 承载的虚拟目录），并加载它们以方便创建配置。  
  
#### <a name="creating-a-configuration-file"></a>创建配置文件  
  
1.  启动服务配置编辑器，通过使用命令窗口导航到你[!INCLUDE[indigo2](../../../includes/indigo2-md.md)]安装位置，然后键入`SvcConfigEditor.exe`。  
  
2.  从**文件**菜单上，选择**打开**单击**可执行文件**， **COM + 服务**，或**WebHosted 服务**，具体取决于你想要创建的配置文件的类型。  
  
3.  在**打开**对话框框中，导航到你想要创建的配置文件，并双击它的特定文件。  
  
4.  在**文件**菜单上，指向**添加新项**单击**服务**。 “新建服务元素向导”随即打开。  
  
5.  按照向导中的步骤创建新服务。  
  
> [!NOTE]
>  如果想要从向导生成的配置文件中使用 NetPeerTcpBinding，您必须手动添加一个绑定配置元素，并将其 `mode` 元素的 `security` 特性设置为“None”。  
  
## <a name="configuring-com"></a>配置 COM+  
 使用服务配置编辑器可以为现有 COM+ 应用程序创建新的配置文件，或者编辑现有的 COM+ 配置。 **COM 协定**节点才可见 <`comContract`> 部分中的配置文件存在。  
  
### <a name="creating-a-new-com-configuration"></a>创建新的 COM+ 配置  
 创建新的 COM+ 配置之前，请确保您的 COM+ 应用程序已安装在 Component Services 中，并已在全局程序集缓存 (GAC) 中注册。  
  
1.  选择**文件**菜单->**集成** -> **COM + 应用程序。** 此操作将关闭当前打开的文件。 如果当前文件中有未保存的数据，将显示“保存”对话框。 **COM + 集成向导**随即启动。  
  
2.  在第一页中，从树中选择 COM+ 应用程序。 如果在树中找不到你的 COM+ 应用程序，请验证它是否已安装在组件服务中，并已在全局程序集缓存 (GAC) 中注册。  
  
3.  在下一页中，选择要公开哪个（哪些）方法作为 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 服务。 默认情况下，COM+ 应用程序中支持的所有方法都将显示并被选中。  
  
4.  选择宿主方法。  
  
5.  根据向导中的指导配置其他设置。  
  
6.  服务配置编辑器在后台利用 ComSvcConfig.exe 来生成配置文件。 此操作完成后，可查看摘要，然后退出向导。 生成的配置文件将打开，您可以直接进行编辑。  
  
### <a name="editing-an-existing-com-configuration"></a>编辑现有 COM+ 配置  
  
1.  选择**文件**菜单->**打开** -> **COM + 服务**...  
  
2.  从列表中选择要编辑的 COM+ 服务。  
  
3.  编辑中的配置设置**COM 协定**节点。  
  
    > [!NOTE]
    >  也可以直接打开并编辑包含 COM 约定的配置文件。  
  
## <a name="security"></a>安全性  
 不能保证配置编辑器生成的服务配置文件是安全的。 请参阅[安全](../../../docs/framework/wcf/feature-details/security.md)文档以了解如何保护你[!INCLUDE[indigo2](../../../includes/indigo2-md.md)]服务。  
  
 此外，只能使用配置编辑器来读取和写入有效的 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 配置元素。 工具将忽略符合架构的用户定义元素。 工具不会尝试从配置文件中移除这些元素，或确定它们对已知 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 元素的影响。 用户需要负责确定这些元素是否会对应用程序或系统构成威胁。
