---
title: in 参数修饰符（C# 参考）
ms.date: 03/06/2018
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
helpviewer_keywords:
- parameters [C#], in
- in parameters [C#]
author: BillWagner
ms.author: wiwagn
ms.openlocfilehash: 3c15cc0dce5b37866fd826e3d6b9adcb00724672
ms.sourcegitcommit: 935d5267c44f9bce801468ef95f44572f1417e8c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/28/2018
---
# <a name="in-parameter-modifier-c-reference"></a>in 参数修饰符（C# 参考）

`in` 关键字通过引用传递参数。 它类似于 [ref](ref.md) 或 [out](out-parameter-modifier.md) 关键字，只是通过调用的方法不能修改 `in` 参数，而可以修改 `ref` 参数，同时 `out` 参数必须由调用方修改，并且在调用上下文中可观测这些修改。

[!code-csharp-interactive[cs-in-keyword](../../../../samples/snippets/csharp/language-reference/keywords/in-ref-out-modifier/InParameterModifier.cs#1)]  

前面的示例说明调用站点处通常不需要 `in` 修饰符。 仅在方法声明中需要它。

> [!NOTE] 
> `in` 关键字还作为 `foreach` 语句的一部分，或作为 LINQ 查询中 `join` 子句的一部分，与泛型类型参数一起使用来指定该类型参数为逆变。 有关在这些上下文使用 `in` 关键字的详细信息，请参阅 [in](in.md)，其中提供了所有这些用法的链接。
  
 作为 `in` 参数传递的变量在方法调用中传递之前必须进行初始化。 但是，所调用的方法可能不会分配值或修改参数。  
  
 尽管 `in`、`ref` 和 `out` 关键字会导致不同的运行时行为，它们并不被视为编译时方法签名的一部分。 因此，如果唯一的不同是一个方法采用 `ref` 或 `in` 参数，而另一个方法采用 `out` 参数，则无法重载这两个方法。 例如，以下代码将不会编译：  
  
```csharp
class CS0663_Example
{
    // Compiler error CS0663: "Cannot define overloaded 
    // methods that differ only on in, ref and out".
    public void SampleMethod(in int i) { }
    public void SampleMethod(ref int i) { }
}
```
  
存在 `in` 时可以重载：  
  
```csharp
class InOverloads
{
    public void SampleMethod(in int i) { }
    public void SampleMethod(int i) { }
}
```

## <a name="overload-resolution-rules"></a>重载决策规则

通过理解使用 `in` 参数的动机，可以理解使用按值方法和使用 `in` 参数方法的重载决策规则。 定义使用 `in` 参数的方法是一项潜在的性能优化。 某些 `struct` 类型参数可能很大，在紧凑的循环或关键代码路径中调用方法时，复制这些结构的成本就很高。 方法声明 `in` 参数以指定参数可能按引用安全传递，因为所调用的方法不修改该参数的状态。 按引用传递这些参数可以避免（可能产生的）高昂的复制成本。 

通常可以选择在调用站点的参数上指定 `in`。 按值传递参数和使用 `in` 修饰符按引用传递参数这两种方法并没有语义差异。 可以在调用站点选择 `in` 修饰符，因为你不需要指出参数值可能会改变。 在调用站点显式添加 `in` 修饰符以确保参数是按引用传递，而不是按值传递。 显式使用 `in` 有两个效果：

首先，在调用站点指定 `in` 会强制编译器选择使用匹配的 `in` 参数定义的方法。 否则，如果两种方法唯一的区别在于是否存在 `in`，则按值重载的匹配度会更高。

第二点，指定 `in` 会声明你想按引用传递参数。 结合 `in` 使用的参数必须代表一个可以直接引用的位置。 `out` 和 `ref` 参数的相同常规规则适用：不能使用常数、普通属性或其他生成值的表达式。 否则，在调用站点省略 `in` 就会通知编译器你将允许它创建临时变量，并按只读引用传递至方法。 编译器创建临时变量以克服一些 `in` 参数的限制：

- 临时变量允许将编译时常数作为 `in` 参数。
- 临时变量允许使用属性或 `in` 参数的其他表达式。
- 存在从实参类型到形参类型的隐式转换时，临时变量允许使用实参。

在前面的所有实例中，编译器创建了临时变量，用于存储常数、属性或其他表达式的值。

以下代码阐释了这些规则：

```csharp
static void Method(in int argument)
{
    // implementation removed
}

Method(5); // OK, temporary variable created.
Method(5L); // CS1503: no implicit conversion from long to int
short s = 0;
Method(s); // OK, temporary int created with the value 0
Method(in s); // CS1503: cannot convert from in short to in int
int i = 42;
Method(i); // passed by readonly reference
Method(in i); // passed by readonly reference, explicitly using `in`
```

现在，假设可以使用另一种使用按值参数的方法。 结果的变化如以下代码所示：

```csharp
static void Method(int argument)
{
    // implementation removed
}

static void Method(in int argument)
{
    // implementation removed
}

Method(5); // Calls overload passed by value
Method(5L); // CS1503: no implicit conversion from long to int
short s = 0;
Method(s); // Calls overload passed by value.
Method(in s); // CS1503: cannot convert from in short to in int
int i = 42;
Method(i); // Calls overload passed by value
Method(in i); // passed by readonly reference, explicitly using `in`
```

最后一个是按引用传递参数的唯一方法调用。

> [!NOTE]
> 为了简化操作，前面的代码将 `int` 用作参数类型。 因为大多数新式计算机中的引用都比 `int` 大，所以将单个 `int` 作为只读引用传递没有任何好处。 

## <a name="limitations-on-in-parameters"></a>`in` 参数的限制

不能将 `in`、`ref` 和 `out` 关键字用于以下几种方法：  
  
- 异步方法，通过使用 [async](async.md) 修饰符定义。  
- 迭代器方法，包括 [yield return](yield.md) 或 `yield break` 语句。  

## <a name="c-language-specification"></a>C# 语言规范  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>请参阅  
 [C# 参考](../index.md)  
 [C# 编程指南](../../programming-guide/index.md)  
 [C# 关键字](index.md)  
 [方法参数](method-parameters.md)[具有值类型的引用语义](../../reference-semantics-with-value-types.md)
