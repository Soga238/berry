---
layout: default
---

# Class

## Class and Instance

Berry provides some object-oriented functionality through classes. Class can be created by C-API or defined using a Berry code. Berry's class consists of some methods and member variables.

## Define a class

Uses keyword `class` definitions class.

``` ruby
class TestClass
end
```

Class is one of the basic types, so a class is also the value stored in a variable.

## Methods and Members

The methods in the class are similar to the function defined with the keyword `def`, and the member variable is defined using the `var` keyword

<div class="highlight"><pre class="highlight"><code><span class="k">class</span> <span class="nc">TestClass</span>
    <span class="k">var</span> <span class="n">a</span> <span class="c1"># define member variable</span>
    <span class="k">def</span> <span class="nf">init</span><span class="p">()</span> <span class="c1"># define method init</span>
        <span class="nb">self</span><span class="p">.</span><span class="nf">a</span> <span class="o">=</span> <span class="mi">0</span>
    <span class="k">end</span>
    <span class="k">def</span> <span class="nf">method</span><span class="p">(</span><span class="n">a</span><span class="p">)</span> <span class="c1"># define method</span>
        <span class="k">return</span> <span class="n">a</span> <span class="o">*</span> <span class="mi">2</span>
    <span class="k">end</span>
<span class="k">end</span>
</code></pre></div>

## Constructor and Instantiation

Berry constructs an instance of the class by calling the class name. Like this

``` ruby
class TestClass
    ...
end
obj = TestClass() # instantiation a class
```

The number of parameters used for instantiation depends on the number of explicit constructor arguments of the class. The explicit constructor of class is the method `init`, where you can define the initialization behavior of the class. When instantiated, the interpreter will constructs an instance object based on the class information. The method `init` has a return value but will not be used when instantiating.

This code demonstrates the explicit constructor of the class and instantiates this class.

``` ruby
1 class Test
2     def init(a)
3         print("structure test", a)
4     end
5 end
6 obj = Test('hello')
7 print(type(obj), classname(obj))
```

The result of this example is

```
structure test hello
instance Test
```

This class is instantiated at sixth line of code and the result is printed with `"structure test hello"`, which means that the method `init` was called during the construction of the class. The 7th line prints the type and class name of the variable `obj`. The results are `instance` and `Test` respectively, which means that the variable `obj` is an instance of the class `Test`.

## Method and Operators Overloading
