---
title: 阵列
ms.date: 12/06/2017
f1_keywords:
- vb.Array
helpviewer_keywords:
- arrays [Visual Basic]
- Visual Basic, arrays
ms.assetid: dbf29737-b589-4443-bee6-a27588d9c67e
ms.openlocfilehash: 9dfe7814b00b4d060fa4ab9aa594faa948217d8d
ms.sourcegitcommit: 17ee6605e01ef32506f8fdc686954244ba6911de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/22/2019
ms.locfileid: "74351867"
---
# <a name="arrays-in-visual-basic"></a>Visual Basic 中的数组

数组是一组值，这些值是逻辑上相互关联的*元素*。 例如，数组可能包含一个语法学校中每个年级的学生数量；数组的每个元素则是单个年级的学生数量。 同样，数组可能包含的一个班的学生的成绩；数组的每个元素则是一个成绩。

可以使用单独的变量来存储每个数据项。 例如，如果应用程序分析学生评分，则可以为每位学生的成绩使用单独的变量，如 `englishGrade1`、`englishGrade2`等。此方法有三个主要限制：

- 我们在设计时必须知道我们需要处理的成绩的总数。
- 处理大量的成绩可导致速度变慢。 反过来，这会使应用程序更有可能出现严重的 bug。
- 很难维护。 我们添加的每个新成绩都要求应用程序进行修改、重新编译和重新部署。

通过使用数组，可以按相同的名称引用这些相关的值，并使用名为*索引*或*下标*的数字来根据元素在数组中的位置来识别单个元素。 数组索引的范围是从 0 到数组中的总元素数 - 1。 当使用 Visual Basic 语法来定义数组的大小时，指定的是其最高的索引值，而不是数组中元素的总数。 可以使用数组作为一个单元，利用循环迭代其元素的功能，你将无需在设计时了解数组确切包含多少个元素。

在进行说明之前，请看几个简单的示例：

```vb
' Declare a single-dimension array of 5 numbers.
Dim numbers(4) As Integer

' Declare a single-dimension array and set its 4 values.
Dim numbers = New Integer() {1, 2, 4, 8}

' Change the size of an existing array to 16 elements and retain the current values.
ReDim Preserve numbers(15)

' Redefine the size of an existing array and reset the values.
ReDim numbers(15)

' Declare a 6 x 6 multidimensional array.
Dim matrix(5, 5) As Double

' Declare a 4 x 3 multidimensional array and set array element values.
Dim matrix = New Integer(3, 2) {{1, 2, 3}, {2, 3, 4}, {3, 4, 5}, {4, 5, 6}}

' Declare a jagged array
Dim sales()() As Double = New Double(11)() {}
```

## <a name="array-elements-in-a-simple-array"></a>简单数组中的数组元素

让我们创建一个名为 `students` 的数组，用于存储语法 school 中每个年级的学生数量。 元素的索引范围为 0 到 6。 使用此数组比声明七个变量更简单。

下图显示了 `students` 数组。 对于数组的每个元素：

- 元素索引表示年级（索引 0 表示幼儿园）。

- 元素中包含的值表示每个年级的学生数量。

![显示学生数数组的关系图](./media/index/students-array-elements.gif)

下面的示例包含创建和使用数组的 Visual Basic 代码：

[!code-vb[simple-array](~/samples/snippets/visualbasic/programming-guide/language-features/arrays/simple-array.vb)]

该示例执行三个操作：

- 它声明了包含七个元素的 `students` 数组。 数组声明中 `6` 的数字指示数组中的最后一个索引;它比数组中的元素数小1。
- 它将值分配给数组中的每个元素。 数组元素通过使用数组名称访问，并在括号中包含单个元素的索引。
- 列出了数组的每个值。 该示例使用[`For`](../../../language-reference/statements/for-next-statement.md)语句，按其索引号访问数组中的每个元素。

上一示例中的 `students` 数组是一维数组，因为它使用一个索引。 使用多个索引或下标的数组称为*多维*。 有关详细信息，请参阅本文的其余部分和[Visual Basic 中的数组维度](../../language-features/arrays/array-dimensions.md)。

## <a name="creating-an-array"></a>创建数组

可以通过多种方式定义数组的大小：

- 可在声明数组时指定大小：

  [!code-vb[creating1](~/samples/snippets/visualbasic/programming-guide/language-features/arrays/create-array.vb#1)]

- 创建数组时，可以使用 `New` 子句提供该数组的大小：

  [!code-vb[creating2](~/samples/snippets/visualbasic/programming-guide/language-features/arrays/create-array.vb#2)]

如果你有现有的数组，则可以通过使用[`ReDim`](../../../language-reference/statements/redim-statement.md)语句来重新定义其大小。 您可以指定 `ReDim` 语句保留数组中的值，也可以指定它创建一个空数组。 下面的示例演示了用 `ReDim` 语句来修改现有数组的大小的不同用法。

[!code-vb[redimensioning](~/samples/snippets/visualbasic/programming-guide/language-features/arrays/create-array.vb#3)]

有关详细信息，请参阅[ReDim 语句](../../../language-reference/statements/redim-statement.md)。

## <a name="storing-values-in-an-array"></a>在数组中存储值

你可以通过使用类型 `Integer`的索引访问数组中的每个位置。 你可以使用括号内的索引来引用每个数组位置，从而存储和检索数组中的值。 多维数组的索引用逗号（，）分隔。 每个数组维度都需要一个索引。

下面的示例演示在数组中存储和检索值的一些语句。

[!code-vb[store-and-retrieve](~/samples/snippets/visualbasic/programming-guide/language-features/arrays/store-and-retrieve.vb)]

## <a name="populating-an-array-with-array-literals"></a>使用数组文本填充数组

通过使用数组文本，可以在创建它时填充具有一组初始值的数组。 数组文本包含用逗号分隔的值列表，这些值被括在括号内 (`{}`)。

通过使用数组文本创建数组时，可以提供数组类型或使用类型推理功能来确定数组类型。 下面的示例演示了这两个选项。

[!code-vb[create-with-literals](~/samples/snippets/visualbasic/programming-guide/language-features/arrays/create-array.vb#4)]

使用类型推理时，数组的类型由文本值列表中的*主导类型*确定。 基准类型是数组中的所有其他类型可以扩大到的类型。 如果无法确定此唯一类型，基准类型将是数组中所有其他类型可以缩小到的唯一类型。 如果无法确定为这两种唯一类型之一，则基准类型是 `Object`。 例如，如果提供给数组文本的值的列表包含 `Integer`、 `Long`和 `Double`类型的值，则生成的数组类型是 `Double`。 由于 `Integer` 和 `Long` 仅放宽 `Double`，因此 `Double` 为主导类型。 有关详细信息，请参阅 [Widening and Narrowing Conversions](../../language-features/data-types/widening-and-narrowing-conversions.md)。

> [!NOTE]
> 只能对定义为类型成员中的局部变量的数组使用类型推理。 如果不存在显式类型定义，则在类级别使用数组文本定义的数组的类型为 `Object[]`。 有关详细信息，请参阅[局部类型推理](../variables/local-type-inference.md)。

请注意，上面的示例将 `values` 定义为类型 `Double` 的数组，即使所有数组文本都为类型 `Integer`。 你可以创建此数组，因为数组文本中的值可以扩大到 `Double` 值。

还可以使用*嵌套的数组文本*来创建和填充多维数组。 嵌套的数组文本必须具有与生成的数组一致的多个维度。 下面的示例通过使用嵌套的数组文本创建一个二维整数数组。

[!code-vb[nested-array-literals](~/samples/snippets/visualbasic/programming-guide/language-features/arrays/create-array.vb#5)]

在使用嵌套的数组文本创建并填充数组时，如果嵌套的数组文本中的元素数不匹配，就会出错。 如果显式声明数组变量时数组文本具有不同数量的维度，也会发生错误。

与处理一维数组相同，使用嵌套的数组文本创建多维数组时，也可以依赖于类型推断。 推断出的类型是所有嵌套级别的所有数组文本中的所有值的基准类型。 下面的示例从 `Integer` 和 `Double`类型的值创建一个 `Double[,]` 类型的二维数组。

[!code-vb[nested-type-inference](~/samples/snippets/visualbasic/programming-guide/language-features/arrays/create-array.vb#6)]

有关其他示例，请参阅[如何：在 Visual Basic 中初始化数组变量](../../language-features/arrays/how-to-initialize-an-array-variable.md)。

## <a name="iterating-through-an-array"></a>循环访问数组

当循环访问数组时，将按从最低到最高或从最高到低的索引顺序访问数组中的每个元素。 通常，使用[For .。。下一语句](../../../language-reference/statements/for-next-statement.md)或[每个 .。。Next 语句](../../../language-reference/statements/for-each-next-statement.md)来循环访问数组的元素。 如果不知道数组的上限，可以调用 <xref:System.Array.GetUpperBound%2A?displayProperty=nameWithType> 方法来获取索引的最大值。 尽管最低索引值几乎始终为0，但您可以调用 <xref:System.Array.GetLowerBound%2A?displayProperty=nameWithType> 方法来获取索引的最小值。

下面的示例通过使用[`For...Next`](../../../language-reference/statements/for-next-statement.md)语句来循环访问一维数组。

[!code-vb[iterate-one-dimensional-array](~/samples/snippets/visualbasic/programming-guide/language-features/arrays/iterate1d.vb)]

下面的示例通过使用[`For...Next`](../../../language-reference/statements/for-next-statement.md)语句来循环访问多维数组。 <xref:System.Array.GetUpperBound%2A> 方法具有用于指定维度的参数。 `GetUpperBound(0)` 返回第一个维度的最高索引，`GetUpperBound(1)` 返回第二个维度的最高索引。

[!code-vb[iterate-two-dimensional-array](~/samples/snippets/visualbasic/programming-guide/language-features/arrays/iterate2d.vb)]

下面的示例使用[For Each .。。](../../../language-reference/statements/for-each-next-statement.md)用于循环访问一维数组和二维数组的 Next 语句。

[!code-vb[iterate-for-each-next](~/samples/snippets/visualbasic/programming-guide/language-features/arrays/iterate-for-each-next.vb)]

## <a name="array-size"></a>数组大小

数组的大小是数组所有维度的长度的产物。 它表示数组中当前所包含的元素总数。  例如，下面的示例声明每个维度中包含四个元素的二维数组。 如示例中的输出所示，数组的大小为16（或（3 + 1） * （3 + 1）。

[!code-vb[array-size](~/samples/snippets/visualbasic/programming-guide/language-features/arrays/array-size.vb)]

> [!NOTE]
> 对数组大小的讨论不适用于交错数组。 有关交错数组和确定交错数组大小的信息，请参阅[交错](#jagged-arrays)数组部分。

可以通过使用 <xref:System.Array.Length%2A?displayProperty=nameWithType> 属性查找数组大小。 您可以使用 <xref:System.Array.GetLength%2A?displayProperty=nameWithType> 方法查找多维数组的每个维度的长度。

您可以通过向数组变量分配新数组对象或使用[`ReDim` 语句](../../../language-reference/statements/redim-statement.md)语句来调整其大小。 下面的示例使用 `ReDim` 语句将100元素数组更改为51元素数组。

[!code-vb[resize-an-array](~/samples/snippets/visualbasic/programming-guide/language-features/arrays/array-size2.vb)]

当处理数组大小时，需要记住几件事情。

|||
|---|---|
|维度长度|每个维度的索引均从 0 开始，这意味着其范围为 0 到其上限之间。 因此，给定维度的长度大于该维度的声明的上限。|
|长度限制|数组的每个维度的长度限制为 `Integer` 数据类型的最大值（<xref:System.Int32.MaxValue?displayProperty=nameWithType> 或（2 ^ 31）-1）。 但是，数组的总大小还受到系统上可用内存的限制。 如果你尝试初始化的数组超过可用内存量，运行时会引发 <xref:System.OutOfMemoryException>。|
|大小和元素大小|数组的大小独立于其元素的数据类型。 大小始终表示元素的总数，而不是所占用的内存的字节数。|
|内存消耗|对于针对数组在内存中的存储情况进行假设，这种做法不可靠的。 由于不同数据宽度的平台上的存储会有所变化，因此同一数组在 64 位系统上可以占用比在 32 位系统上更多的内存。 基于初始化数组时的系统配置，公共语言运行时 (CLR) 可能会分配存储空间以尽可能近地将元素打包在一起，或者将它们全部在自然硬件边界上对齐。 此外，数组需要用于其控制信息的存储开销，此开销会在每次增加维度时随之增加。|

## <a name="the-array-type"></a>数组类型

每个数组的数据类型均不同于其元素的数据类型。 没有一种数据类型能用于所有数组。 相反，数组的数据类型由数组的维度数量或 *“排名”* ，以及数组中元素的数据类型确定。 仅当两个数组具有相同的秩并且其元素具有相同的数据类型时，两个数组变量才具有相同的数据类型。 数组的维度的长度不会影响数组的数据类型。

每个数组都继承自 <xref:System.Array?displayProperty=nameWithType> 类，并且你可以声明一个类型为 `Array`的变量，但不能创建一个类型为 `Array`的数组。 例如，尽管下面的代码将 `arr` 变量声明为类型 `Array`，并调用 <xref:System.Array.CreateInstance%2A?displayProperty=nameWithType> 方法来实例化数组，数组的类型会证明是 Object []。

[!code-vb[array-class](~/samples/snippets/visualbasic/programming-guide/language-features/arrays/array-class.vb)]

此外，[ReDim 语句](../../../language-reference/statements/redim-statement.md)无法对声明为类型 `Array` 的变量执行运算。 出于这些原因，以及为了保证类型安全，建议将每个数组声明为特定类型。

可以通过几种方式确定数组及其元素的数据类型。

- 您可以对变量调用 <xref:System.Object.GetType%2A> 方法，以获取表示变量的运行时类型的 <xref:System.Type> 对象。 <xref:System.Type> 对象可在其属性和方法中保存大量信息。
- 可以将变量传递给 <xref:Microsoft.VisualBasic.Information.TypeName%2A> 函数，以获取具有运行时类型名称的 `String`。

下面的示例调用 `GetType` 方法和 `TypeName` 函数来确定数组的类型。 数组类型为 `Byte(,)`。 请注意，<xref:System.Type.BaseType%2A?displayProperty=nameWithType> 属性还指示字节数组的基类型是 <xref:System.Array> 类。

[!code-vb[array-type](~/samples/snippets/visualbasic/programming-guide/language-features/arrays/array-type.vb)]

## <a name="arrays-as-return-values-and-parameters"></a>数组作为返回值和参数

若要通过 `Function` 过程返回数组，请将数组数据类型和维度数指定为 [Function 语句](../../../language-reference/statements/function-statement.md)的返回类型。 在函数内，声明一个具有相同数据类型和维度数的局部数组变量。 在 [Return 语句](../../../language-reference/statements/return-statement.md)中，添加不带括号的局部数组变量。

若要将作为参数的数组指定到 `Sub` 或 `Function` 步骤中，可将此参数定义为具有指定数据类型和维度数量的数组。 在对该过程的调用中，传递一个具有相同数据类型和维度数的数组变量。

在下面的示例中，`GetNumbers` 函数返回 `Integer`类型的一维数组 `Integer()`。 `ShowNumbers` 过程接受 `Integer()` 参数。

[!code-vb[return-value-and-params](~/samples/snippets/visualbasic/programming-guide/language-features/arrays/return-values-and-params.vb)]

在下面的示例中，`GetNumbersMultiDim` 函数返回 `Integer`类型的二维数组 `Integer(,)`。  `ShowNumbersMultiDim` 过程接受 `Integer(,)` 参数。

[!code-vb[multidimensional-return-value](~/samples/snippets/visualbasic/programming-guide/language-features/arrays/return-values-and-params-2d.vb)]

## <a name="jagged-arrays"></a>交错数组

有时应用程序中的数据结构是二维而不是矩形。 例如，可能会使用数组来存储当月每天高温的相关数据。 该数组的第一个维度表示月份，而第二个维度表示天数，并且一个月内的天数是不一致的。 *交错数组*（也称为*数组*）是为这种情况设计的。 交错数组的元素也是数组。 交错数组和交错数组中的每个元素都可以具有一个或多个维度。

下面的示例使用月份数组，其中的每个元素是天数的数组。 该示例使用交错数组，因为不同月份有不同的天数。  示例演示如何创建交错数组，将值分配给它，并检索和显示它的值。

[!code-vb[jagged-arrays](~/samples/snippets/visualbasic/programming-guide/language-features/arrays/jagged.vb)]

前面的示例通过使用 `For...Next` 循环，为逐个元素地将值分配给交错数组。 通过使用嵌套的数组文本，还可以将值分配给交错数组的元素。 不过，尝试使用嵌套的数组文本（例如 `Dim valuesjagged = {{1, 2}, {2, 3, 4}}`）会生成编译器错误[BC30568](../../../,,/../misc/bc30568.md)。 若要更正此错误，请将内部数组文本用括号括起来。 圆括号会强制计算数组文本表达式，生成的值会用于外部数组文本，如以下示例所示。

[!code-vb[jagged-array-initialization](~/samples/snippets/visualbasic/programming-guide/language-features/arrays/jagged-assign.vb)]

交错数组是一维数组，其元素包含数组。 因此，<xref:System.Array.Length%2A?displayProperty=nameWithType> 属性和 `Array.GetLength(0)` 方法返回一维数组中的元素数，`Array.GetLength(1)` 将引发 <xref:System.IndexOutOfRangeException>，因为交错数组不是多维的。 通过检索每个子数组的 <xref:System.Array.Length%2A?displayProperty=nameWithType> 属性的值，可以确定每个子数组中的元素数。 下面的示例演示如何确定交错数组中的元素数。

[!code-vb[jagged-array-size](~/samples/snippets/visualbasic/programming-guide/language-features/arrays/jagged-length.vb)]

## <a name="zero-length-arrays"></a>长度为零的数组

Visual Basic 在未初始化的数组（值为 `Nothing`的数组）和*零长度数组*或空数组（没有元素的数组）之间区分开来。未初始化的数组是指尚未对其进行尺寸或分配任何值的数组。 例如：

```vb
Dim arr() As String
```

零长度数组的声明维度为 -1。 例如：

```vb
Dim arrZ(-1) As String
```

在下列情况下，你可能需要创建一个零长度数组：

- 如果不冒 <xref:System.NullReferenceException> 异常，你的代码必须访问 <xref:System.Array> 类的成员，如 <xref:System.Array.Length%2A> 或 <xref:System.Array.Rank%2A>，或调用 Visual Basic 函数（如 <xref:Microsoft.VisualBasic.Information.UBound%2A>）。

- 您希望通过不必将 `Nothing` 作为一种特殊情况进行检查来使代码保持简单。

- 你的代码与应用程序编程接口 (API) 交互，该接口要求你将一个零长度数组传递到一个或多个过程，或将一个零长度数组返回到一个或多个过程。

## <a name="splitting-an-array"></a>拆分数组

在某些情况下，可能需要将单个数组拆分为多个数组。 这涉及到确定数组的一个或多个分割点，然后将数组分割为两个或更多的数组。

> [!NOTE]
> 本部分不讨论如何将单个字符串基于某些分隔符拆分为字符串数组。 有关拆分字符串的信息，请参阅 <xref:System.String.Split%2A?displayProperty=nameWithType> 方法。

拆分数组最常见的条件是：

- 数组中的元素数。 例如，你可能想要将一个元素数超过指定值的数组拆分为多个大小大致相等的数组。 为此，可以使用 <xref:System.Array.Length%2A?displayProperty=nameWithType> 或 <xref:System.Array.GetLength%2A?displayProperty=nameWithType> 方法返回的值。

- 元素的值，该值充当分隔符，用于指示数组的分割点。 可以通过调用 <xref:System.Array.FindIndex%2A?displayProperty=nameWithType> 和 <xref:System.Array.FindLastIndex%2A?displayProperty=nameWithType> 方法来搜索特定值。

确定应拆分数组的索引或索引后，可以通过调用 <xref:System.Array.Copy%2A?displayProperty=nameWithType> 方法来创建各个数组。

下面的示例将数组拆分成两个大小大致相等的数组。 （如果数组元素的总数为奇数，则第一个数组比第二个数组多一个元素。）

[!code-vb[splitting-an-array-by-length](~/samples/snippets/visualbasic/programming-guide/language-features/arrays/split1.vb)]

下面的示例根据值为“zzz”的元素（充当数组分隔符）的存在情况将一个字符串数组拆分成两个数组。 新数组不包括包含分隔符的元素。

[!code-vb[splitting-an-array-by-delimiter](~/samples/snippets/visualbasic/programming-guide/language-features/arrays/split2.vb)]

## <a name="joining-arrays"></a>合并数组

还可以将多个数组合并为一个较大的数组。 为此，你还可以使用 <xref:System.Array.Copy%2A?displayProperty=nameWithType> 方法。

> [!NOTE]
> 本部分不讨论将单个字符串联接到单个字符串的相关信息。 有关联接字符串数组的信息，请参阅 <xref:System.String.Join%2A?displayProperty=nameWithType> 方法。

在将每个数组的元素复制到新数组前，首先必须确保已初始化了该数组，确保它有足够的空间来容纳新数组。 可以通过两种方法执行此操作：

- 在将新元素添加到数组之前，请使用[`ReDim Preserve`](../../../language-reference/statements/redim-statement.md)语句以动态方式扩展该数组。 这是最简单的方法，但在复制大型数组时可能会导致性能下降并占用过多内存。
- 计算新大型数组所需的元素总数，然后将每个源数组的元素添加到其中。

以下示例使用第二种方法将分别具有 10 个元素的四个数组添加到一个数组中。

[!code-vb[joining-an-array](~/samples/snippets/visualbasic/programming-guide/language-features/arrays/join.vb)]

由于在这种情况下，源数组都是小的，因此我们还可以在将每个新数组的元素添加到数组时，动态扩展数组。 以下示例执行该操作。

[!code-vb[joining-an-array-dynamically](~/samples/snippets/visualbasic/programming-guide/language-features/arrays/join2.vb)]

## <a name="collections-as-an-alternative-to-arrays"></a>作为数组的替代方法的集合

数组最适用于创建和使用固定数量的强类型化对象。 集合提供更灵活的方式来使用对象组。 与数组不同，数组要求使用[`ReDim` 语句](../../../language-reference/statements/redim-statement.md)显式更改数组的大小，集合随着应用程序更改的需要动态地增长和收缩。

使用 `ReDim` 对数组进行重维数时，Visual Basic 创建新数组，并释放以前的数组。 这需要执行时间。 因此，如果需要频繁进行更改，或者不能预测所需的最大项数，则通常应使用集合来获得更好的性能。

对于某些集合，你可以为放入集合中的任何对象分配一个关键字，这样你便可以使用该关键字快速检索此对象。

如果你的集合中只包含一种数据类型的元素，你可以使用 <xref:System.Collections.Generic?displayProperty=nameWithType> 命名空间中的一个类。 泛型集合强制类型安全，因此无法向其添加任何其他数据类型。

有关集合的详细信息，请参阅[集合](../../concepts/collections.md)。

## <a name="related-topics"></a>相关主题

|术语|Definition|
|----------|----------------|
|[Array Dimensions in Visual Basic](../../language-features/arrays/array-dimensions.md)|在数组中解释级别和维度。|
|[如何：在 Visual Basic 中初始化数组变量](../../language-features/arrays/how-to-initialize-an-array-variable.md)|说明如何用初始值填充数组。|
|[如何：在 Visual Basic 中对数组进行排序](../../language-features/arrays/how-to-sort-an-array.md)|显示如何按字母先后顺序对数组元素进行排序。|
|[如何：将一个数组赋给另一个数组](../../language-features/arrays/how-to-assign-one-array-to-another-array.md)|说明将数组分配到另一个数组变量的规则和步骤。|
|[数组疑难解答](../../language-features/arrays/troubleshooting-arrays.md)|讨论在使用数组时出现的一些常见问题。|

## <a name="see-also"></a>另请参阅

- <xref:System.Array?displayProperty=nameWithType>
- [Dim 语句](../../../language-reference/statements/dim-statement.md)
- [ReDim 语句](../../../language-reference/statements/redim-statement.md)
