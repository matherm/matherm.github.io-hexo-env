---
title: Fast and efficient way to blog with and about function plots
date: 2017-10-27 21:57:50
mathjax: true
tags:
  - Function Plots
categories:
  - Comparison
  - Blog
---
I am looking for a JavaScript-Library that makes plotting of more or less simple functions easy. From a quick Google search I got some different options that I will test throughout this post.
- [Function Plotter](https://mauriciopoppe.github.io/function-plot/)
- [d3.js](https://d3js.org/)
- [p5.js](https://p5js.org/)
- [plotly.js](https://plot.ly/javascript/)
- [Blogging with IPython](http://blog.fperez.org/2012/09/blogging-with-ipython-notebook.html) *very curious about that*

For the whole comparison of the different libraries I will use the Binary Entropy Function, which has the following definition:
$$
H(X) = H_b(p) = -p \log_2 p -(1-p) \log_2 (1-p)
$$

<!-- more --> 

Beside the Binary Entropy function I'd like additionally test simple point and random variable plots. 
For my simple point plot I will use the following data $S = {(3,4),(5,6),(10,8),(9,3),(4,4),(8,8)}$. My random variable will be a Normal Distribution $X \sim \mathcal{N}(0,1)\,.$

# Round 1: Function Plotter
Let us begin with the Function Plotter Library.

{% blockquote Mauricio Poppe https://mauriciopoppe.github.io/function-plot/ f(x)-Function Plot %}
Function Plot is a plotting library built on top of D3.js used to render functions with little configuration (think of it as a clone of Google's plotting utility: y=x2y=x2)
{% endblockquote %} 

As Function Plotter is a JavaScript-Library we first have to embed custom JavaScript-Code into Hexo. This is done by the tags ``{ % raw %}``and ``{ % endraw %}``. Inside these tags we can embed arbitrary HTML-code.

{% codeblock lang:HTML %}
{ % raw %} //Remove space between { and %
<script src="https://cdnjs.cloudflare.com/ajax/libs/d3/3.5.5/d3.min.js"></script>
<script src="https://wzrd.in/standalone/function-plot@1.18.1"></script>
<div id=quadratic></div>
<script>
    functionPlot({
    target: '#quadratic',
    data: [{
        fn: 'x^2'
        }]
    })
</script>
{ % endraw %} //Remove space between { and %
{% endcodeblock %}

This snippet produces the following really cool result. 
{% raw %}
<script src="https://cdnjs.cloudflare.com/ajax/libs/d3/3.5.5/d3.min.js"></script>
<script src="https://wzrd.in/standalone/function-plot@1.18.1"></script>
<div id=quadratic></div>
<script>
    functionPlot({
    target: '#quadratic',
    data: [{
        fn: 'x^2'
        }]
    })
</script>
{% endraw %}

***To be continued...***