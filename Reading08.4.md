## Reading 8.4

## Omega和摊销分析

在本节中，我们将结束对渐近的讨论。**大部分内容要到课程后期才会展开。**本节扩展了 Big O 的概念并介绍了 Omega。我们还将探讨摊销运行时的概念及其分析。最后，我们将以对运行时的实证分析和复杂性理论的预演结束。

### 运行时分析细节

**练习：**R( N )是 dup3 的运行时间（N是数组长度），那么R(N)的时间复杂度如何？

```java
public boolean dup3(int[] a) {
    int N = a.length;
    for (int i = 0; i < N; i += 1) {
        for (int j = 0; j < N; j += 1) {
            if (a[i] == a[j]) {
                return true;
            }
        }
    }
    return false;
}
```

**回答：** *R* ( *N* ) ∈ Θ ( 1 )，它是恒定的时间！那是因为 dup3 中有一个错误：它总是将第一个元素与自身进行比较。在第一次迭代中，i 和 j 都是 0，所以函数总是立即返回。无赖！

让我们修复 dup4 中的错误，然后再试一次。

**练习：**R( N )是 dup4 的运行时间（N是数组长度），那么R(N)的时间复杂度如何？

```java
public boolean dup4(int[] a) {
    int N = a.length;
    for (int i = 0; i < N; i += 1) {
        for (int j = i + 1; j < N; j += 1) {
            if (a[i] == a[j]) {
                return true;
            }
        }
    }
    return false;
}
```

**答：**这一次，运行时间不仅取决于输入的长度，还取决于数组的内容。

在最好的情况下，R* ( *N* ) ∈ Θ ( 1 )。如果输入数组包含所有相同的元素，那么无论它有多长，dup4 都会在第一次迭代时返回。

另一方面，在最坏的情况下，R( *N* ) ∈ Θ ( *N*^2 ). 如果数组没有重复，则 dup4 永远不会提前返回，嵌套的 for 循环将导致二次运行时。

这个练习突出了 Big Theta 的一个限制。Big Theta 不能直接表示为输入大小N的函数，还需要考虑输入的数组的顺序。

然而，如果运行时不仅仅取决于输入的大小，那么我们必须在使用 Big Theta 之前将我们的语句限定为不同的情况。Big O 消除了这种烦恼。不必描述最好和最坏的情况，对于上面的例子，我们可以简单地说 dup4 的运行时间是O(N^2)，有时 dup4 更快，但最坏的情况是二次方。

#### 一言以蔽之，我们用θ的话，就必须说：

#### 在最坏情况下是：θ..；在最好情况下是：θ..

#### 而Big O 消除了这种烦恼。不必描述最好和最坏的情况，对于上面的例子，我们可以简单地说 dup4 的运行时间是O(N^2)，有时 dup4 更快，但反正最坏的情况是二次方。

## Big Omega 滥用

考虑以下陈述：

1. 酒店最贵的房间是每晚639美元。
2. 酒店每间客房每晚不超过639美元。

哪项陈述为您提供了有关酒店的更多信息？

第一个。

第二个语句只提供了房价的上限，即一个不等式。

第一条语句不仅告诉您房价的上限，而且还告诉您已达到该上限。

例如，考虑一家便宜的酒店，其最贵的房间是 89 美元/晚，而一家昂贵的酒店最贵的房间是 639 美元/晚。两家酒店都满足第二个声明，但第一个声明将其范围缩小到后一个酒店。

**练习：**哪条语句为您提供了有关一段代码运行时的更多信息？

1. 最坏情况的运行时间是 Θ(N^2)。

2. 运行时间为 O(N^2)。

**答：**与酒店问题类似，第一个陈述提供了更多信息。考虑以下方法：

```java
public static void printLength(int[] a) {
    System.out.println(a.length);
}
```

这个简单的方法和 dup4 都有运行时O(N^2)，所以知道陈述 2 将无法区分这些。但是语句 1 更精确，并且仅适用于 dup4。

在现实世界中，并且经常在对话中，Big O 经常用于 Big Theta 会提供更多信息的地方。我们看到了一个很好的理由——它使我们无需使用限定语句。

然而，虽然较宽松的说法是正确的，但它不如 Big θ 有用。

**注意：大 O 与“最坏情况”不同。但它经常被这样使用。**

**总结一下 Big O 的用处：**

- **在不同输入的运行时间不同的情况下，它允许我们做出没有大小写限定的简单语句。**
- **有时，对于特别棘手的问题，我们（计算机科学界）不知道确切的运行时间，所以我们可能只声明一个上限。**
- **为 Big O 编写证明比 Big θ 容易得多，就像我们在上一章中找到合并排序的运行时所看到的那样。这超出了本课程的范围。**

### Big Ω （Omega）—— Big O 的补集

为了完善我们对运行时的理解，我们还定义了 Big O 的补集，以描述下限。

虽然 Big Theta 可以非正式地认为是运行时相等，而 Big O 代表“小于或等于”，但 Big Omega 可以被认为是“大于或等于”。

 For example, in addition to knowing that N^3 + 3N^4 \in \Theta(N^4)*N*3+3*N*4∈Θ(*N*4), all of the following statements are true: N^3 + 3N^4 \in \Omega(N^4)*N*3+3*N*4∈Ω(*N*4) N^3 + 3N^4 \in \Omega(N^3)*N*3+3*N*4∈Ω(*N*3) N^3 + 3N^4 \in \Omega(\log N)*N*3+3*N*4∈Ω(log*N*) N^3 + 3N^4 \in \Omega(1)*N*3+3*N*4∈Ω(1)

There's two common uses for Big Omega:

1. It's used to prove Big Theta runtime. If R(N) = O(f(N))*R*(*N*)=*O*(*f*(*N*)) and R(N) = \Omega(f(N))*R*(*N*)=Ω(*f*(*N*)), then R(N) = \Theta(f(N))*R*(*N*)=Θ(*f*(*N*)). Sometimes, it's easier to prove O and \OmegaΩ separately. This is outside the scope of this course.
2. It's used to prove the difficulty of a problem. For example, ANY duplicate-finding algorithm must be \Omega(N)Ω(*N*), because the algorithm must at least look at each element.

Here's a table to summarize the three Big letters:

|                          | Informal Meaning                                 | Example Family     | Example Family Members                                    |
| :----------------------- | :----------------------------------------------- | :----------------- | :-------------------------------------------------------- |
| Big Theta<br>Θ(*f*(*N*)) | Order of growth is f(N)                          | \Theta(N^2)Θ(*N*2) | N^2/2, 2N^2, N^2 + 38N + 1/N*N*2/2,2*N*2,*N*2+38*N*+1/*N* |
| Big <br>O*(*f*(*N*))     | Order of growth is less than or equal to f(N)    | O(N^2)*O*(*N*2)    | N^2/2, 2N^2, \log N*N*2/2,2*N*2,log*N*                    |
| Big Omega<br>Ω(*f*(*N*)) | Order of growth is greater than or equal to f(N) | \Omega(N^2)Ω(*N*2) | N^2/2, 2N^2, 5^N*N*2/2,2*N*2,5*N*                         |

## 摊销分析（直观解释）

#### 格里戈麦斯的骨灰盒

格里戈麦斯是一只看起来有点恐怖的恶魔犬。他让你能够在梦中出现在马的面前，就像他有时会出现在你的梦和中期一样。然而，作为这种能力的回报，你必须定期向他提供一瓮瓮干草作为贡品。他为您提供了两种付款方式：

- 选择 1：每天，格里戈麦斯从你的瓮中吃掉 3 蒲式耳的干草。
- 选择 2：随着时间的推移，Grigometh 吃的干草呈指数级增长，**但来的频率呈指数级下降。**具体来说：
  - 第 1 天，他吃了 1 蒲式耳干草（共 1 蒲式耳）
  - 第 2 天，他又吃了 2 蒲式耳干草（共 3 蒲式耳）
  - p.s. 第三天没来
  - 第 4 天，他又吃了 4 蒲式耳干草（共 7 蒲式耳）
  - 第 8 天，他又吃了 8 蒲式耳干草（共 15 蒲式耳）

您想制定一个例行程序，每天在您的骨灰盒中放入固定数量的干草。对于每个付款计划，您每天必须投入多少干草？哪个更便宜？

对于第一个选择，您每天必须在骨灰盒中放入 3 蒲式耳干草。然而，实际上第二个选择要便宜一点！您每天只需在骨灰盒中放入 2 蒲式耳干草即可。（试着说服自己为什么这是真的——一种方法是写下你每天贡献的干草总量。你会注意到，每当格里戈麦斯来吃他的干草零食时，他吃饱后，骨灰盒里多了蒲式耳。）

抛开蒲式耳不谈，请注意，Grigometh 每天的干草消耗量实际上是恒定的，在选择 2 中，我们可以将这种情况描述为**摊销的恒定**干草消耗量。

#### AList 调整大小和摊销

事实证明，Grigometh 的干草困境与 AList 在课程早期调整大小非常相似。回想一下，在基于数组的列表的实现中，当我们在底层数组已满的 AList 上调用 add 方法时，我们需要调整数组的大小。换句话说，add 方法在满时必须创建一个更大的新数组，复制旧元素，然后最后添加新元素。我们的新阵列应该大多少？回想以下两个实现：

实施1

```java
public void addLast(int x) {
  if (size == items.length) {
    resize(size + RFACTOR);
  }
  items[size] = x;
  size += 1;
}
```

实施 2

```java
public void addLast(int x) {
  if (size == items.length) {
    resize(size * RFACTOR);
  }
  items[size] = x;
  size += 1;
}
```

第一个实现结果非常糟糕。当我们的数组填满时，每次添加一个新元素时，都必须将整个数组复制到一个新元素中。

另一方面，我们称之为几何调整大小的第二种实现效果很好。事实上，这就是 Python 列表的实现方式。

让我们更详细地研究实现 2 的运行时。令 RFACTOR 为 2。当数组已满时，调整大小使其大小翻倍。大多数添加操作需要θ ( 1 )时间，但有些非常昂贵，并且与当前大小成线性关系。**但是，如果我们平均所有廉价添加的调整大小的昂贵添加的成本，并且考虑到昂贵的添加每次发生的频率减半（这正和上面的恐怖犬的故事一致），结果表明，平均而言，添加的运行时间是θ ( 1 ). 我们将在下一节中证明这一点。同时，这里有一张图表来说明这一点：**

![amortized_add_operations](https://joshhug.gitbooks.io/hug61b/content/assets/amortized_adds.png)

## 摊销分析（严谨解释）

**这里对摊销分析进行了更严格的检查，分三个步骤：**

1. **选择一个成本模型（如常规运行时分析）**

   ```java
   //比如例子如下
   for(int i = 0; i < N; i++){
   	System.out.print("hello");
   }
   //那么在这个例子中，我们的成本模型就是System.out.print("hello");
   ```

2. **计算第 i 个操作的平均成本**

3. **证明这个平均（摊销）成本受一个常数的限制。**

**举个例子，假设最初我们的 ArrayList 包含一个长度为 1 的数组。让我们将这三个步骤应用于 ArrayList 调整大小：**

1. 对于我们的成本模型，我们将只考虑数组读取和写入。（您还可以在成本模型中包含其他操作，例如数组创建和填充默认数组值的成本。但事实证明，这些都会产生相同的结果。）
2. 让我们计算一系列数组添加的成本。假设我们有以下代码：

- x.add(0) 执行 1 次写入操作。没有调整大小。总计：1 次操作
- x.add(1) 调整大小并复制现有数组（1 次读取，1 次写入），然后写入新元素。总计：3 次操作
- x.add(2) 调整大小并复制现有数组（2 次读取，2 次写入），然后写入新元素。总计：5 次操作
- x.add(3) 不会调整大小，只会写入新元素。总计：1 次操作
- x.add(4) 调整大小并复制现有数组（4 次读取，4 次写入），然后写入新元素。总计：9 次操作

在表格中更容易跟踪这一点：

|                             |      |      |      |      |      |      |      |      |      |      |      |      |      |      |
| :-------------------------- | :--- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
| 插入                        | 0    | 1    | 2    | 3    | 4    | 5    | 6    | 7    | 8    | 9    | 10   | 11   | 12   | 13   |
| a[i] 写入成本               | 1    | 1    | 1    | 1    | 1    |      |      |      |      |      |      |      |      |      |
| 插入引起的调整大小/复制成本 | 0    | 2    | 4    | 0    | 8    |      |      |      |      |      |      |      |      |      |
| 总费用                      | 1    | 3    | 5    | 1    | 9    |      |      |      |      |      |      |      |      |      |
| 累计成本                    | 1    | 4    | 9    | 10   | 19   |      |      |      |      |      |      |      |      |      |

**练习：**填写此表的其余部分。总成本是一个特定插入的总成本。累积成本是迄今为止所有插入的成本。

**回答：**

| 插入 ＃           | 0    | 1    | 2    | 3    | 4    | 5    | 6    | 7    | 8    | 9    | 10   | 11   | 12   | 13   |
| :---------------- | :--- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
| a[i] 写入成本     | 1    | 1    | 1    | 1    | 1    | 1    | 1    | 1    | 1    | 1    | 1    | 1    | 1    | 1    |
| 调整大小/复制成本 | 0    | 2    | 4    | 0    | 8    | 0    | 0    | 0    | 16   | 0    | 0    | 0    | 0    | 0    |
| # 的总费用        | 1    | 3    | 5    | 1    | 9    | 1    | 1    | 1    | 17   | 1    | 1    | 1    | 1    | 1    |
| 累计成本          | 1    | 4    | 9    | 10   | 19   | 20   | 21   | 22   | 39   | 40   | 41   | 42   | 43   | 44   |

那么一系列添加的平均成本是多少？对于 13 次添加，此平均成本是每个添加为44/13 = 3.14。但是对于前 8 个添加，平均成本是每个添加为：39/8 = 4.875。

3. 平均（摊销）成本是否受常数限制？似乎它可能以 5 为界。但仅通过查看前 13 个添加，我们不能完全确定。

   

我们现在将介绍**“电势”**的概念来帮助我们解决这个摊销之谜。对于每个操作 i，例如每次 add，让ci是某个操作的真实成本，而ai是操作的摊销成本。（也就是说，ai是一个常数，并且对于所有 i 必须是相同的。）

Let Φ*i* be the potential at operation i, which is the cumulative difference between amortized and true cost: Φ*i*=Φ*i*−1+*ai*−*ci*

ai is an arbitrary constant, meaning we can chose it. **If we chose ai such that Φi is never negative and ai is constant for all i, then the amortized cost is an upper bound on the true cost.** And if the true cost is upper bounded by a constant, then we've shown that it is on average constant time!

**让我们假设每天的均摊消耗是3，然后假设电势初始值是0（这个问题中的电势指的就是假设每天放入3干草，那么每天实际剩下的稻草数就是电势），那么最终情况如下**

| Day (i)                  | 1    | 2    | 3    | 4    | 5    | 6    | 7    | 8    | 9    | 10   | 11   | 12   | 13   | 14   |
| :----------------------- | :--- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
| Actual cost c_i*c**i*    | 1    | 2    | 0    | 4    | 0    | 0    | 0    | 0    | 8    | 0    | 0    | 0    | 0    | 0    |
| Amortized cost a_i*a**i* | 3    | 3    | 3    | 3    | 3    | 3    | 3    | 3    | 3    | 3    | 3    | 3    | 3    | 3    |
| Change in potential      | +2   | +1   | +3   | -1   | +3   | +3   | +3   | +3   | -5   | +3   | +3   | +3   | +3   | +3   |
| Potential Φ*i*           | 2    | 3    | 6    | 5    | 8    | 11   | 14   | 17   | 12   | 15   | 18   | 21   | 24   | 27   |

如果我们让ai = 3，电势（干草势）永远不会变成负数——事实上，如果我们每天增加 3 蒲式耳，看起来很多天后，我们将继续为 Grigometh 提供剩余的干草。我们将把这一点的严格证明留到另一门课上，但希望这个趋势看起来足够令人信服。所以格里戈麦斯的干草贡品平均来说是恒定的。

**练习：**我们希望尽可能多地保存干草。以此证明我们可以满足 Grigometh 的饥饿感，并且即使我们设置了ai为更小的情况，比如 ai = 2，也永远不会有负电势出现。

## 现在让我们回到 ArrayList 调整大小

**练习：**ArrayList 添加操作的ci是多少？如果我们让链表操作的摊余成本ai = 5，电势会变成负数吗？是否还有其他较小的摊销成本有效？填写一张像格里戈麦斯那样的表格来帮助解决这个问题。

**回答：** ci 是数组调整大小和添加新元素的总成本，如果 i 是 2 的幂次，ci = 2i + 1。否则ci = 1，如下图所示：

| Insert #            | 0    | 1    | 2    | 3    | 4    | 5    | 6    | 7    | 8    | 9    | 10   | 11   | 12   | 13   |
| :------------------ | :--- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
| Actual cost ci      | 1    | 3    | 5    | 1    | 9    | 1    | 1    | 1    | 17   | 1    | 1    | 1    | 1    | 1    |
| Amortized cost ai   | 5    | 5    | 5    | 5    | 5    | 5    | 5    | 5    | 5    | 5    | 5    | 5    | 5    | 5    |
| Change in potential | 4    | 2    | 0    | 4    | -4   | 4    | 4    | 4    | -12  | 4    | 4    | 4    | 4    | 4    |
| Potential Φ*i*      | 4    | 6    | 6    | 10   | 6    | 10   | 14   | 18   | 6    | 10   | 14   | 18   | 22   | 26   |

通过观察趋势，电势永远不应该是负面的（省略了这方面的证据）。直觉上，对于高成本的操作（resize），我们利用之前的低成本操作（add）来储存电势。

最后，我们展示了 ArrayList 添加操作确实是摊销的常数时间。几何调整大小（乘以 RFACTOR）导致良好的列表性能。

### 概括

- Big O 是一个上限（“小于或等于”）
- Big Omega 是一个下限（“大于或等于”）
- Big Theta 既是上限又是下限（“等于”）
- Big O 并不意味着“最坏情况”。我们仍然可以使用 Big Theta 来描述最坏的情况
- Big Omega 并不意味着“最好的情况”。我们仍然可以使用 Big Theta 来描述最佳情况
- 有时在 Big Theta 可以提供更精确的陈述的情况下通俗地使用 Big O
- 摊销分析提供了一种证明平均运行时成本的方法。
- 如果我们假设了一个 ai，使得 iΦ 永远不会是负数，并且 ai 对所有操作都是恒定的，那么摊销成本 ai 就是真实成本的上限。

