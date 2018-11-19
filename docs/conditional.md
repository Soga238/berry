---
layout: default
---

# Conditional Statements

Berry提供if语句来实现条件控制执行的功能。if语句通过条件表达式的真假来决定控制流。

## if语句

**`if`语句**的形式如下

``` ruby
if (condition)
    block
end
```

在`if`语句的条件判断中，如果条件为真则执行分支下的block，否则会跳过该block。如果执行了分支下的block，block中的最后一条语句执行完以后会离开`if`语句。

**`if else`**语句的形式是

<div class="highlight"><pre class="highlight"><code><span class="k">if</span> <span class="p">(</span><span class="n">condition</span><span class="p">)</span>
    <span class="n">block</span>
<span class="k">else</span>
    <span class="n">block</span>
<span class="k">end</span>
</code></pre></div>
<div class="highlight"><pre class="highlight"><code><span class="k">if</span> <span class="p">(</span><span class="n">condition</span><span class="p">)</span>
    <span class="n">block</span>
<span class="k">elif</span>
    <span class="n">block</span>
<span class="k">else</span>
    <span class="n">blocak</span>
<span class="k">end</span>
</code></pre></div>
<div class="highlight"><pre class="highlight"><code><span class="k">if</span> <span class="p">(</span><span class="n">condition</span><span class="p">)</span>
    <span class="n">block</span>
<span class="k">elif</span>
    <span class="n">block</span>
<span class="k">end</span>
</code></pre></div>

在上面几种表达式中，`elif`可以在`if`条件及`else`之间出现0到多次，而`if`条件只在开头出现一次，`else`在最后最多出现一次。与`if`语句相似，在`if`和`elif`条件判定为真时，会执行相应分支下的block，否则会测试下一个分支。当执行完某个分支的block之后，会离开整个`if else`语句（也就是执行`end`之后的语句）。

Berry的`if`语句必须使用一个`end`关键字来表示结束，而所有的代码块会被包含在`if`, `elif`, `else`以及`end`之间。这么做的原因是保证程序的执行路径唯一，防止语法解析的时候出现二义性。