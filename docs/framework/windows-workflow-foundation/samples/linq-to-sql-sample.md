---
title: LINQ to SQL 示例
ms.date: 03/30/2017
ms.assetid: 5f39db9e-0e62-42c9-8c98-bb8b54cec98c
ms.openlocfilehash: a5c84dab941a50ddd5edb065004343cc304fd0f3
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="linq-to-sql-sample"></a>LINQ to SQL 示例
此示例演示如何创建活动以使用 LINQ to SQL 查询 SQL Server 数据库的表中的实体。  
  
> [!IMPORTANT]
>  您的计算机上可能已安装 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 示例。 在继续操作之前，请先检查以下（默认）目录：  
>   
>  `<InstallDrive>:\Samples\WCFWFCardspace`  
>   
>  如果该目录不存在，请单击此页顶部的下载示例链接。 请注意，此链接将下载和安装所有 [!INCLUDE[wf1](../../../../includes/wf1-md.md)]、[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 和 [!INCLUDE[infocard](../../../../includes/infocard-md.md)] 示例。 此示例位于以下目录：  
>   
>  `<InstallDrive>:\Samples\WCFWFCardSpace\WF\Scenario\ActivityLibrary\Linq\LinqToSql`  
  
## <a name="activity-details-for-findinsqltable"></a>FindInSqlTable 的活动详细信息  
 此活动允许用户使用 LINQ to SQL 查询数据库的表中的实体。 此活动的用户还可以提供 lambda 表达式形式的 LINQ 谓词来筛选结果。 如果未提供谓词，则返回整个表。 下表详述了此活动的属性和返回值。  
  
|属性或返回值|描述|  
|------------------------------|-----------------|  
|`Collection` 属性|必需属性，用于指定源集合。|  
|`Predicate` 属性|必需属性，用于指定 lambda 表达式形式的集合筛选器。|  
|返回值|经过筛选的集合。|  
  
## <a name="code-sample-that-uses-the-custom-activity"></a>使用自定义活动的代码示例  
 下面的代码示例使用 `FindInSqlTable` 自定义活动，在名为 `Employee` 的 SQL Server 表中查找所有 `Role` 列等于 `SDE` 的行。  
  
```csharp  
new FindInSqlTable<Employee>   
{  
    ConnectionString = @"Data Source=.\SQLExpress;Initial Catalog=LinqToSqlSample;Integrated Security=True",                          
    Predicate = new LambdaValue<Func<Employee, bool>>(c => new Func<Employee, bool>(emp => emp.Role.Equals("SDE"))),  
    Result = new OutArgument<IList<Employee>>(employees)  
},  
```  
  
#### <a name="to-use-this-sample"></a>使用此示例  
  
1.  打开命令提示。  
  
2.  导航到包含此示例的文件夹。  
  
3.  运行 Setup.cmd 命令文件。  
  
    > [!NOTE]
    >  Setup.cmd 脚本尝试将此示例数据库安装在您本地计算机上的 SQL Server Express 中。 如果您需要在其他 SQL Server 实例中安装它，请编辑 Setup.cmd。  
  
     Setup.cmd 脚本执行以下操作：  
  
    -   创建一个名为 LinqToSqlSample 的数据库。  
  
    -   创建一个 Roles 表。  
  
    -   创建一个 Employees 表。  
  
    -   将 3 个记录插入到 Roles 表中。  
  
    -   将 12 个记录插入到 Employees 表中。  
  
4.  使用 [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] 打开 LinqToSQL.sln 解决方案文件。  
  
5.  要生成解决方案，按 Ctrl+Shift+B。  
  
6.  若要运行解决方案，请按 F5。  
  
#### <a name="to-uninstall-the-linqtosql-sample-database"></a>卸载 LinqToSql 示例数据库  
  
1.  打开命令提示。  
  
2.  导航到包含此示例的文件夹。  
  
3.  运行 Cleanup.cmd 命令文件。  
  
> [!IMPORTANT]
>  您的计算机上可能已安装这些示例。 在继续操作之前，请先检查以下（默认）目录：  
>   
>  `<InstallDrive>:\WF_WCF_Samples`  
>   
>  如果此目录不存在，请转到[Windows Communication Foundation (WCF) 和针对.NET Framework 4 的 Windows Workflow Foundation (WF) 示例](http://go.microsoft.com/fwlink/?LinkId=150780)下载所有 Windows Communication Foundation (WCF) 和[!INCLUDE[wf1](../../../../includes/wf1-md.md)]示例。 此示例位于以下目录：  
>   
>  `<InstallDrive>:\WF_WCF_Samples\WF\Scenario\ActivityLibrary\Liiinq\LinqToSql`  
  
## <a name="see-also"></a>请参阅  
 [LINQ to SQL](http://go.microsoft.com/fwlink/?LinkId=150376)  
 [入门 (LINQ to SQL)](http://go.microsoft.com/fwlink/?LinkId=150377)
