# 变量词项

在 [term.md](term.md "mention")一节中，原子词项、陈述、复合词项被定义出来，其中的最小单位是原子词项，而原子词项的形式是词语。某些时候，一个陈述中可能包含某个词项，该词项希望被用于指代其他词项，此时则需要使用“变量”。

> **定义2.5.** 一个**变量原子词项**是用于指代其他词项的原子词项，其形式为“$$前缀~变量名$$”，其中“$$前缀$$”一部分决定了变量被处理的方式，变量名的形式是词语(word)。

变量原子词项是一种特殊的原子词项，为了以示区分，非变量的原子词项也被称为常量原子词项。但在不加说明时，原子词项通常指的是常量原子词项。

> **定义2.6.** 变量的作用域(scope)是包含该变量所有出现处的最小词项。

例如，若我们定义某系词的形式为“$$\rightarrow$$”，其直观含义是“是一种”，并定义某系词的形式为“$$\Rightarrow$$”，其直观含义是“如果...那么...”，则“如果知更鸟是一种鸟，那么知更鸟是一种动物”被表示为“$$\langle \langle robin \rightarrow bird  \rangle \Rightarrow \langle  robin \rightarrow animal \rangle \rangle$$”。若我们定义某种变量的前缀为“$$ \$ $$”，其含义是“任意的”，则“如果任意的某物是一种鸟，那么该物是一种动物”被表示为“$$\langle \langle \$x \rightarrow bird  \rangle \Rightarrow \langle  \$x \rightarrow animal \rangle \rangle$$”。这里“$$\$ x$$”就是一个变量原子词项（定义2.5），其前缀为“$$ \$ $$”，其变量名为“$$x$$”，该变量的作用域就是陈述“$$\langle \langle \$x \rightarrow bird  \rangle \Rightarrow \langle  \$x \rightarrow animal \rangle \rangle$$”，而“$$\langle \$x \rightarrow bird  \rangle$$”则不是，因为该变量还出现在了陈述“$$\langle \$x \rightarrow animal\rangle$$”中。

假如系统中存在另一陈述“$$\langle \langle \$x \rightarrow robin \rangle \Rightarrow \langle  \$x \rightarrow bird \rangle \rangle$$”，其直观含义是“如果任意的某物是一种知更鸟，那么该物是一种鸟”，尽管它包含了变量“$$\$x$$”，但此处的变量与上面的变量并非同一物，尽管变量名相同，它们有着不同的作用域。

我们举这一例子是为了理解定义2.5和2.6，尽管引入了两个“系词”和一个变量的前缀，这两个系词将在[relation](../relation/ "mention")一节中正式介绍，而变量的不同前缀将紧接着在下面介绍。







