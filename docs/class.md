---
layout: default
---

# Class

### Class and Instance

Berry provides some object-oriented functionality through classes. Class can be created by C-API or defined using a Berry script. Berry's class consists of several methods and member variables.

#### Define a class

Uses keyword `class` definitions class.

``` ruby
class TestClass
end
```

Class is stored in the variable table of the scope in which it is defined, just like any other type.

#### Methods and Members

The methods in Class are similar to the general function `def` initions, which defare defined using keywords in the class block , and the member variables need to be defined using `var` keywords

<div class="highlight"><pre class="highlight"><code><span class="k">class</span> <span class="nc">TestClass</span>
    <span class="k">var</span> <span class="n">a</span> <span class="c1"># define member variable</span>
    <span class="k">def</span> <span class="nf">init</span><span class="p">()</span> <span class="c1"># 定义init方法</span>
        <span class="nb">self</span><span class="p">.</span><span class="nf">a</span> <span class="o">=</span> <span class="mi">0</span>
    <span class="k">end</span>
    <span class="k">def</span> <span class="nf">method</span><span class="p">(</span><span class="n">a</span><span class="p">)</span> <span class="c1"># define method</span>
        <span class="k">return</span> <span class="n">a</span> <span class="o">*</span> <span class="mi">2</span>
    <span class="k">end</span>
<span class="k">end</span>
</code></pre></div>

#### Constructor and Instantiation

Berry gets an instance by calling the name of the class.

``` ruby
class TestClass
    ...
end
obj = TestClass() # instantiation a class
```

The number of parameters used for instantiation depends on the number of explicit constructor arguments of the class. The explicit constructor of Class is a `init` method, you can define the initialization behavior of the class in the class. When instantiated, the interpreter will generate an instance object based on the class information. Berry allows initmethods to have a return value but will not be used when instantiating.
