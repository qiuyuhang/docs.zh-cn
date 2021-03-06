---
title: 从 XML 架构派生数据集关系结构 (XSD)
ms.date: 03/30/2017
ms.assetid: 8f6cd04d-6197-4bc4-9096-8c51c7e4acae
ms.openlocfilehash: 7599577c4e0f485e336e7f79a6c3bd17f0f0c316
ms.sourcegitcommit: 11f11ca6cefe555972b3a5c99729d1a7523d8f50
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="deriving-dataset-relational-structure-from-xml-schema-xsd"></a>从 XML 架构派生数据集关系结构 (XSD)
本节将概述如何从 XML 架构定义语言 (XSD) 架构文档生成 `DataSet` 的关系架构。 一般情况下，为每个`complexType`的架构元素的子元素，在生成一个表`DataSet`。 表结构取决于复杂类型的定义。 在中创建表`DataSet`架构中的顶级元素。 但是，仅为创建了表的顶级`complexType`元素时`complexType`元素嵌套在另一个`complexType`元素，在这种情况下嵌套`complexType`元素映射到`DataTable`内`DataSet`。  
  
 有关 XSD 的更多信息，请参阅万维网联合会 (W3C) XML 架构第 0 部分： 入门建议，XML 架构第 1 部分： 结构建议和 XML 架构第 2 部分： 数据类型建议，位于[ http://www.w3.org/](http://www.w3.org/TR/).  
  
 下面的示例演示一个 XML 架构其中`customers`是的子元素`MyDataSet`元素，它是**数据集**元素。  
  
```xml  
<xs:schema id="SomeID"   
            xmlns=""   
            xmlns:xs="http://www.w3.org/2001/XMLSchema"   
            xmlns:msdata="urn:schemas-microsoft-com:xml-msdata">  
   <xs:element name="MyDataSet" msdata:IsDataSet="true">  
     <xs:complexType>  
       <xs:choice maxOccurs="unbounded">  
         <xs:element name="customers" >   
           <xs:complexType >  
             <xs:sequence>  
               <xs:element name="CustomerID" type="xs:integer"   
                            minOccurs="0" />  
               <xs:element name="CompanyName" type="xs:string"   
                            minOccurs="0" />  
               <xs:element name="Phone" type="xs:string" />  
             </xs:sequence>  
           </xs:complexType>  
          </xs:element>  
       </xs:choice>  
     </xs:complexType>  
   </xs:element>  
 </xs:schema>  
```  
  
 在上例中，`customers` 元素为复杂类型元素。 因此，将对复杂类型定义进行分析，而映射过程会创建下表。  
  
```  
Customers (CustomerID , CompanyName, Phone)  
```  
  
 该表中各列的数据类型是从所指定的相应元素或属性的 XML 架构类型派生的。  
  
> [!NOTE]
>  如果元素`customers`是简单的 XML 架构数据类型的如**整数**，不生成任何表。 表仅为属于复杂类型的顶级元素而创建。  
  
 在下面的 XML 架构中，**架构**元素具有两个元素子级，`InStateCustomers`和`OutOfStateCustomers`。  
  
```xml  
<xs:schema id="SomeID"   
            xmlns=""   
            xmlns:xs="http://www.w3.org/2001/XMLSchema"   
            xmlns:msdata="urn:schemas-microsoft-com:xml-msdata">  
   <xs:element name="InStateCustomers" type="customerType" />  
   <xs:element name="OutOfStateCustomers" type="customerType" />  
    <xs:complexType name="customerType" >  
  
     </xs:complexType>  
  
   <xs:element name="MyDataSet" msdata:IsDataSet="true">  
     <xs:complexType>  
       <xs:choice maxOccurs="unbounded">  
         <xs:element ref="customers" />  
       </xs:choice>  
     </xs:complexType>  
   </xs:element>  
 </xs:schema>  
```  
  
 `InStateCustomers` 和 `OutOfStateCustomers` 两个子元素都是复杂类型元素 (`customerType`)。 因此，映射过程生成中的以下两个相同表格`DataSet`。  
  
```  
InStateCustomers (CustomerID , CompanyName, Phone)  
OutOfStateCustomers (CustomerID , CompanyName, Phone)  
```  
  
## <a name="in-this-section"></a>本节内容  
 [将 XML 架构 (XSD) 约束映射到数据集约束](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/mapping-xml-schema-xsd-constraints-to-dataset-constraints.md)  
 描述用于创建唯一约束和外键约束中的 XML 架构元素`DataSet`。  
  
 [从 XML 架构生成数据集关系 (XSD)](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/generating-dataset-relations-from-xml-schema-xsd.md)  
 描述用于创建表中各列之间的关系的 XML 架构元素`DataSet`。  
  
 [XML 架构约束和关系](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/xml-schema-constraints-and-relationships.md)  
 描述如何关系创建隐式使用 XML 架构元素创建中的约束时`DataSet`。  
  
## <a name="related-sections"></a>相关章节  
 [在数据集中使用 XML](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/using-xml-in-a-dataset.md)  
 介绍如何加载和保持的关系结构和中的数据`DataSet`以 XML 数据形式。  
  
## <a name="see-also"></a>请参阅  
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)
