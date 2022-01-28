### Lists2 Study Guide

## 概述

**裸数据结构** `IntLists`很难使用。为了 `IntList`正确使用，程序员必须理解和利用递归，即使是简单的列表相关任务。

**添加衣服**首先，我们将`IntList`类变成一个`IntNode` 类。然后，我们将删除`IntNode`类中的所有方法。接下来，我们将创建一个名为 的新类`SLList`，其中包含实例变量 `first`，并且该变量的类型应为`IntNode`。本质上，我们用`SLList`就是在用`IntNode`.

**使用 SLList**作为用户，为了创建一个列表，我调用 的构造函数 `SLList`，并传入我希望用来填充列表的数字。然后`SLList` 构造函数将调用`IntList`具有该编号的构造函数，并设置 `first`为指向`IntList`它刚刚创建的。

**改进**请注意，在创建具有一个值的列表时，我们编写了 `SLList list = new SLList(1)`. 我们不必像处理`IntList`. 本质上， SLList 类充当列表用户和裸露之间的中间人`IntList`。

**Public vs. Private**我们希望用户`SLList`只通过方法来修改我们的列表，而不是直接修改`first`. 我们可以通过设置我们的变量访问权限来阻止其他用户这样做`private`。编写`private IntNode first;`可以防止其他类中的代码访问和修改`first` （而类中的代码仍然可以这样做）。

**嵌套类**我们还可以将类移动到类中来制作嵌套类！**您也可以将嵌套类声明为私有；这样，其他类永远不能使用这个嵌套类。**

**静态嵌套类  如果`IntNode`该类从不使用该类的任何变量或方法`SLList`，我们可以通过添加“static”关键字将该类变为静态。**

**递归辅助方法**如果我们想在 中编写一个递归方法 `SLList`，我们将如何去做呢？毕竟，`SLList`不是像`IntNode`. 一个常见的想法是编写一个用户可以调用的外部方法。此方法调用`IntNode`作为参数的私有辅助方法。然后，此辅助方法将执行递归，并将答案返回给外部方法。

**缓存**`IntList`以前，我们通过返回 1 + 列表其余部分的大小来递归计算我们的大小。如果我们的列表变得非常大，这会变得非常慢，并且我们反复调用我们的 size 方法。现在我们有了`SLList`，让我们简单地将列表的大小缓存为实例变量！请注意，如果没有 out ，我们之前无法做到这一点`IntList`。

**空列表**有了`SLList`，我们现在可以表示一个空列表。我们只需设置`first`to`null`和`size`to `0`。但是，我们引入了一些错误；也就是说，因为`first`is now `null`，任何尝试访问`first`(like `first.item`) 属性的方法都将返回 a `NullPointerException`。当然，我们可以通过编写处理这种特殊情况的代码来修复这个错误。但可能有很多特殊情况。有更好的解决方案吗？

**哨兵节点**让所有`SLList`对象，甚至是空列表，都一样。为此，让我们给每个 SLList 一个哨兵节点，一个始终存在的节点。实际元素在哨兵节点之后。此外，我们所有的方法都应该尊重哨兵始终是我们列表中的第一个元素的想法。

**不变量**不变量是关于保证为真的数据结构的事实（假设您的代码中没有错误）。每次我们向数据结构中添加功能时，这都会为我们提供一个方便的清单。用户还可以保证他们信任的某些属性将得到维护。例如，`SLList`带有哨兵节点的 an 至少具有以下不变量：

- 哨兵引用始终指向哨兵节点。
- 最前面的项目（如果存在）总是在 sentinel.next.item。
- size 变量始终是已添加的项目总数。

## 练习

### C级

1. 完成[在线教科书](https://joshhug.gitbooks.io/hug61b/content/chap2/chap22.html)中的练习。
2. 重新解释哨兵节点是什么以及为什么它很重要。问问自己，如果您删除了哨兵，您的代码是否会出错。哨兵是您的 IntList 的必要组成部分吗？
3. 没有大小变量而是每次只计算大小的缺点是什么？

### B级

1. 从讲座代码存储库中提供给您的 SLList.java 副本开始，实现方法`deleteFirst`，该方法将删除 SLList 中的第一个元素。不要忘记维护上面讨论的三个不变量。
2. 从讲座代码存储库中提供给您的 SLList.java 的副本开始，实现第二个构造函数，该构造函数接受一个整数数组，并使用这些整数创建一个 SLList。再次，记住保持你的不变量。
3. 如果哨兵节点是一个空节点，它会改变任何东西还是 Intlist 能够运行？

### A级

1. [从 Kartik教科书](http://www.kartikkapur.com/documents/mt1.pdf#page=7)的期中 1 开始做第 5 题

2. 修改 Intlist 类，以便每次添加值时都“平方” IntList。例如，在插入 5 后，下面的 IntList 将从：

   1 => 2 比 1 => 1 => 2 => 4 => 5

   如果将 7 添加到后者的 IntList 中，它将变为

   1 => 1 => 1 => 1 => 2 => 4 => 4 => 16 => 5 => 25 => 7

   此外，还为您提供了在添加节点的整个过程中只能访问一次 size() 函数的约束。