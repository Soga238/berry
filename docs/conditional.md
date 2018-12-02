---
layout: default
---

# Conditional Statements

Berry provides an `if` statement to implement conditional control execution. The `if` statement determines the control flow by the `true` and `false` of the conditional expression.

## if Statement

The form of the **`if` statement** is as follows

``` ruby
if (condition)
    block
end
```

In the conditional test of the `if` statement, if the condition is true, the block following this branch is executed, otherwise the block is skipped. If the block following the branch is executed, the last statement in the block will leave the `if` statement after execution.

The form of the **`if else` statement** is as follows

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

In the above statements, `elif` can appear 0 to many times between the `if` condition and `else`, and the `if` condition only appears once at the beginning, and `else` appears at most at the end. Similar to the `if` statement, when the `if` and `elif` conditions are true, the block following the corresponding branch is executed, otherwise the next branch is tested. When the block of a branch is executed, it will leave the `if else` statement (the statement after `end` will be executed).

Berry's `if` statement must end with an `end` keyword, and all blocks are contained between `if`, `elif`, `else`, and `end`. This ensures that the execution path is unique and prevents ambiguity.
