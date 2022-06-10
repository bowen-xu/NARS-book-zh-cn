# 词项

非公理逻辑是由范畴逻辑、集合论等理论发展或借鉴而来，在知识表示上与它们有些许相似之处。其中原子词项是非公理逻辑中表征某个对象的最基本单位，通过某种表示词项间关系的词连接，两个词项以某种形式组织成一条陈述；通过某种表示词项间关系的词连接，多个词项以另某种形式组织成一条复合词项。原子词项、陈述、复合词 项统称为词项。下面将对上述涉及到的概念做更严格的说明。

为了描述复杂的对象，我们从描述语言的最基本单位，即原子词项，开始。

> **定义2.1.** 原子词项(atomic term) 的形式是词语(word)。

在英文场景下，词语是指字母表中的字符构成的字符串，在中文场景下，词语是指汉字构成的字符串。例如，“乌鸦”、“企鹅”、“鸟”、“动物”、“raven”、“penguin” 、“bird”、“animal”等都是原子词项。

原子词项的代码实现如下。类`Term`的成员变量`type`记录了词项的类型，`type`为`Atom`表示该词项为原子词项。类`Term`的成员变量`word`记录了定义2.1中所述的“词语”。为了方便词项被进一步处理，每个词项由一个哈希值`hash_value`唯一标记，该哈希值是通过对字符串`word`的哈希计算得到。

{% tabs %}
{% tab title="Python" %}
{% code title="Narsese/Term.py" %}
```python
class Term:
    type = TermType.ATOM
    # ...
        
    def __init__(self, word, do_hashing=False, word_sorted=None, is_input=False) -> None:
        self.word = word
        # ...
        
        if do_hashing:
            self.do_hashing()
        else:
            self._hash_value = None
```
{% endcode %}
{% endtab %}

{% tab title="C++" %}
{% code title="Narsese/Term.h" %}
```cpp
class Term
{
public:
    TermType type = TermType::ATOM;
    // ...
    
public:
    Term() {}
    Term(char* _word, bool do_hashing=false, bool is_input=false);
    Term(string _word, bool do_hashing, bool is_input);
    // ...
};
```
{% endcode %}

{% code title="Narsese/Term.cpp" %}
```cpp
Term::Term(char *_word, bool do_hashing, bool is_input) : Term(string(_word), do_hashing, is_input) {}

Term::Term(string _word, bool _do_hashing, bool is_input): word(_word)
{
    if (_do_hashing)
    {
        do_hashing();
    }
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

<details>

<summary>创建词项的方法</summary>

通过例如以下代码，即可创建一个原子词项

Python:

```python
from Narsese import Term
term = Term("bird")
print(term)
```

C++:

```cpp
#include "Narsese/Term.h"
using TERM::Term;
term = Term("bird");
std::cout << term.word << endl;
```

</details>

词项以某种方式组织起来形成陈述，正如词语以某种方式组织起来形成简单的语句：

> **定义2.2.** 陈述(statement)是的形式是“$$S 系词 P$$”，其中系词(copula) 的含义是两个词项之间的关系。系词前的原子词项$$S$$被称为主项(subject term或subject)，系词后的词项$$P$$被称为谓项(predicate term或predicate)。

{% tabs %}
{% tab title="Python" %}
{% code title="Narsese/Statement.py" %}
```python
class Statement(Term):
    type = TermType.STATEMENT
    
    def __init__(self, subject: Term, copula: Copula, predicate: Term, is_input: bool=False) -> None:
        self._is_commutative = copula.is_commutative
        word = "<"+str(subject)+str(copula.value)+str(predicate)+">"
        if self.is_commutative:
            subject_word, predicate_word = sorted((subject, predicate), key=hash)
            word_sorted = "<"+subject_word.word_sorted+str(copula.value)+predicate_word.word_sorted+">"
        else: word_sorted = "<"+subject.word_sorted+str(copula.value)+predicate.word_sorted+">"

        self.subject = subject
        self.copula = copula
        self.predicate = predicate

```
{% endcode %}
{% endtab %}

{% tab title="C++" %}

{% endtab %}
{% endtabs %}



复合词项被定义来描述单个或多个词项之间的关系，例如交集关系、并集关系、差集关系等。

> **定义2.3.** 复合词项的形式是，其中连词(connector)的含义是词项之间的关系，该连词连接了一个或多个词项，其中每一个词项被称为该一阶复合词项的成员(component)。

{% tabs %}
{% tab title="Python" %}
```
# TODO
```
{% endtab %}

{% tab title="C++" %}
```
// TODO
```
{% endtab %}
{% endtabs %}

目前我们已经涉及了原子词项、陈述、复合词项的概念，它们可以用一个更宽泛的概念来指代。

> **定义2.4.** 原子词项、陈述、复合词项都是词项(term)。

尽管定义2.2、2.3、2.4有循环定义的嫌疑，然而在工程上，这并不是一个严重的问题。一条纳思语的文本将会被一个语法解析器解析为内部表示，这一递归的过程终止于原子词项。

