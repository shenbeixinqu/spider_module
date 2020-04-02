## pyquery

![img](https://s0.lgstatic.com/i/image3/M01/75/81/Cgq2xl5vH7eAUuuVAALNRJmaBGA830.png)



运行结果如下:

![img](https://s0.lgstatic.com/i/image3/M01/75/81/CgpOIF5vH7eAaT1AAAE9bYyUfNc162.png)

### url初始化

初始化的参数不仅可以以字符串的形式传递，还可以传入网页的 URL，此时只需要指定参数为 url 即可：

![img](https://s0.lgstatic.com/i/image3/M01/75/81/Cgq2xl5vH7eAECJPAAB6T8H4tnI823.png)

运行结果:

![img](https://s0.lgstatic.com/i/image3/M01/75/81/CgpOIF5vH7eALGddAABJynzVLHc637.png)

### 文件初始化

![img](https://s0.lgstatic.com/i/image3/M01/75/81/Cgq2xl5vH7iAGKfaAABx7RJdJfU430.png)

### 基本css选择器

![img](https://s0.lgstatic.com/i/image3/M01/75/81/CgpOIF5vH7iAGChDAANnEEahAxk729.png)

运行结果:

![img](https://s0.lgstatic.com/i/image3/M01/75/81/Cgq2xl5vH7iAE8GWAAFitjSl_80633.png)

直接遍历这些节点，然后调用 text 方法，就可以获取节点的文本内容:

![img](https://s0.lgstatic.com/i/image3/M01/75/81/CgpOIF5vH7iACERfAABnP--G72s108.png)

运行结果:

![img](https://s0.lgstatic.com/i/image3/M01/75/81/Cgq2xl5vH7iASlBtAABNBLt8rZ8125.png)

### 子节点

查找子节点用find方法,传入的参数是css选择器

![img](https://s0.lgstatic.com/i/image3/M01/75/81/CgpOIF5vH7iAHWU1AADEAuCYKdg626.png)

运行结果:

![img](https://s0.lgstatic.com/i/image3/M01/75/81/Cgq2xl5vH7iAAs7DAAUTfPhYvA0606.png)

首先，我们通过.list参数选取class为list的节点，然后调用find方法，传入CSS选择器，选取其内部的li节点，最后打印输出。可以发现，find方法会将符合条件的所有节点选择出来,结果的类型是pyquery类型.

find的查找范围是节点的所有子孙节点,如果只想查找子节点,可以用children方法:

![img](https://s0.lgstatic.com/i/image3/M01/75/81/CgpOIF5vH7mAbzNgAABUf8OMxpI243.png)

运行结果:

![img](https://s0.lgstatic.com/i/image3/M01/75/81/Cgq2xl5vH7mAHAd6AAFj9YG-WMk552.png)

如果要筛选所有子节点中符合条件的节点，比如想筛选出子节点中 class 为 active 的节点，可以向 children 方法传入 CSS 选择器 .active，代码如下：

![img](https://s0.lgstatic.com/i/image3/M01/75/81/CgpOIF5vH7mAIi9xAABMPpFjo0k126.png)

运行结果:

![img](https://s0.lgstatic.com/i/image3/M01/75/81/Cgq2xl5vH7mAd9IgAAC1267P4vw994.png)

### 父节点

我们可以用parent方法来获取某个节点的父节点

![img](https://s0.lgstatic.com/i/image3/M01/75/81/CgpOIF5vH7mASWioAAOlaHUlvY8086.png)

运行结果:

![img](https://s0.lgstatic.com/i/image3/M01/75/81/Cgq2xl5vH7mAOi1yAALTI6WIquo982.png)

如果想要获取祖孙节点,可以用parents方法:

![img](https://s0.lgstatic.com/i/image3/M01/75/81/CgpOIF5vH7mAQsRlAACt6lH-X3Y366.png)

运行结果:

![img](https://s0.lgstatic.com/i/image3/M01/75/81/Cgq2xl5vH7mAZ7MbAAVLxoiz97o679.png)

如果想要筛选某个祖先节点的话，可以向 parents 方法传入 CSS 选择器，这样就会返回祖先节点中符合 CSS 选择器的节点：

![img](https://s0.lgstatic.com/i/image3/M01/75/81/CgpOIF5vH7qAbJATAABRFzeJgBI008.png)

运行结果:

![img](https://s0.lgstatic.com/i/image3/M01/75/81/Cgq2xl5vH7qAPm2WAAK4LVCwLPA373.png)

### 兄弟节点

如果要获取兄弟节点，可以使用 siblings 方法

![img](https://s0.lgstatic.com/i/image3/M01/75/81/CgpOIF5vH7qAPWxlAACGDJd5yUQ383.png)

选择class为list的节点，内部class为item-0和active的节点，也就是第3个li节点。很明显，它的兄弟节点有4个，那就是第1、2、4、5个li...

![img](https://s0.lgstatic.com/i/image3/M01/75/81/Cgq2xl5vH7qAGntQAADopBIUYus244.png)

### 遍历

pyquery 的选择结果既可能是多个节点，也可能是单个节点，类型都是 pyquery 类型，并没有返回列表。

对于单个节点来说，可以直接打印输出，也可以直接转成字符串：

![img](https://s0.lgstatic.com/i/image3/M01/75/81/CgpOIF5vH7qAeMTcAACKTriJIEQ107.png)

运行结果:

![img](https://s0.lgstatic.com/i/image3/M01/75/81/Cgq2xl5vH7qAQ-6CAADGNo64UcY628.png)

对于有多个节点的结果，我们就需要用遍历来获取了。例如，如果要把每一个 li 节点进行遍历，需要调用 items 方法：

![img](https://s0.lgstatic.com/i/image3/M01/75/81/CgpOIF5vH7uAPUrDAACgwrtfw3o139.png)

运行结果:

![img](https://s0.lgstatic.com/i/image3/M01/75/81/Cgq2xl5vH7uAP8z5AAIIHFmybQQ988.png)

可以发现，调用items方法后，会得到一个生成器，遍历一下，就可以逐个得到li节点对象了，它的类型也是pyquery类型。每个li节点还可以调用前面所说的方法进行选择，比如继续查询子节,寻找某个祖先节点.

### 获取信息

提取到节点之后，我们的最终目的当然是提取节点所包含的信息了。比较重要的信息有两类，一是获取属性，二是获取文本，下面分别进行说明。

### 获取属性

提取到某个 pyquery 类型的节点后，就可以调用 attr 方法来获取属性：

![img](https://s0.lgstatic.com/i/image3/M01/75/81/CgpOIF5vH7uAV2BMAAOB6hUfOhM294.png)

运行结果:

![img](https://s0.lgstatic.com/i/image3/M01/75/81/Cgq2xl5vH7uAcyQmAACLQzfPSyk688.png)

也可以通过attr属性来获取属性值

![img](https://s0.lgstatic.com/i/image3/M01/75/81/CgpOIF5vH7uAdtLdAAAthERYa3g542.png)

如果选中的是多个元素,然后调用attr方法,会出现什么样的结果呢?

![img](https://s0.lgstatic.com/i/image3/M01/75/81/CgpOIF5vH7uAINxZAABqoe3cHzQ296.png)

运行结果:

![img](https://s0.lgstatic.com/i/image3/M01/75/81/Cgq2xl5vH7uAbIo7AAGFuHGCZsM074.png)

照理来说，我们选中的a节点应该有4个，打印结果也应该是4个，但是当我们调用attr方法时，返回结果却只有第1个。这是因为，当返回结果包含多个节点时，调用attr方法，只会得到第1个节点的属性

那么，遇到这种情况时，如果想获取所有的 a 节点的属性，就要用到前面所说的遍历了：

![img](https://s0.lgstatic.com/i/image3/M01/75/81/CgpOIF5vH7yAWP6QAACRar_eAQE762.png)

运行结果:

![因此，在进行属性获取时，先要观察返回节点是一个还是多个，如果是多个，则需要遍历才能依次获取每个节点的属性。

### 获取文本

获取节点之后的另一个主要操作就是获取其内部文本了，此时可以调用 text 方法来实现：

![img](https://s0.lgstatic.com/i/image3/M01/75/81/CgpOIF5vH7yAe0SGAANnTI3RefE209.png)

运行结果:

![img](https://s0.lgstatic.com/i/image3/M01/75/82/Cgq2xl5vH7yAKnBKAABiyi-58K0237.png)

如果想要获取这个节点内部的html文本,就要使用html方法

![img](https://s0.lgstatic.com/i/image3/M01/75/81/CgpOIF5vH7yAbYf4AACKPsWr3Ws310.png)

这里我们选中第 3 个 li 节点，然后调用 html 方法，它返回的结果应该是 li 节点内的所有 HTML 文本。

运行结果：

![img](https://s0.lgstatic.com/i/image3/M01/75/82/Cgq2xl5vH7yACqQFAABZLYV0RCc195.png)

如果我们选中的结果是多个节点，text 或 html 方法会返回什么内容？

![img](https://s0.lgstatic.com/i/image3/M01/75/82/Cgq2xl5vH7yAcsmAAANM3eysuuU525.png)

运行结果:

![img](https://s0.lgstatic.com/i/image3/M01/75/81/CgpOIF5vH7yAeTGmAABwbpUI6eE863.png)

如果你想要得到的结果是多个节点，并且需要获取每个节点的内部 HTML 文本，则需要遍历每个节点。而 text 方法不需要遍历就可以获取，它将所有节点取文本之后合并成一个字符串。

### 节点操作

pyquery 提供了一系列方法来对节点进行动态修改，比如为某个节点添加一个 class，移除某个节点等，这些操作有时会为提取信息带来极大的便利。

### addclass,removeclass

![img](https://s0.lgstatic.com/i/image3/M01/75/82/Cgq2xl5vH7yAQEHUAAPKG5e2GHo742.png)

运行结果:

![img](https://s0.lgstatic.com/i/image3/M01/75/81/CgpOIF5vH72AFfgAAAEPKQJQEew788.png)

### attr,text,html

当然，除了操作 class 这个属性外，也可以用 attr 方法对属性进行操作。此外，我们还可以用 text 和 html 方法来改变节点内部的内容

![img](https://s0.lgstatic.com/i/image3/M01/75/82/Cgq2xl5vH72AZFnbAAKEmMT0DT4070.png)

运行结果:

![img](https://s0.lgstatic.com/i/image3/M01/75/81/CgpOIF5vH72AD3L1AAIwylwJzTk879.png)

### remove

![现在我们想提取“Hello,World”这个字符串，该怎样操作呢？这里先直接尝试提取class为wrap的节点的内容，看看是不是我们想要的。运行结果如下：Hello,World This is a paragraph

这个结果还包含了内部的 p 节点的内容，也就是说 text 把所有的纯文本全提取出来了。

![img](https://s0.lgstatic.com/i/image3/M01/75/81/CgpOIF5vH72AVpWfAABSf6CWpsE569.png)

### 伪类选择器

![img](https://s0.lgstatic.com/i/image3/M01/75/81/CgpOIF5vH72AH4XrAASCPBdl_qU793.png)

在这个例子中我们使用了CSS3的伪类选择器，依次选择了第1个li节点、最后一个li节点、第2个li节点、第3个li之后的li节点、偶数位置的li节点、包含second文本的li节点

