---
title: Hello Blog..
date: 2017-10-27 14:45:10
mathjax: true
tags:
  - Test
  - Intro
categories:
  - Blog
---
This Blog is hosted on [GitHub Pages](https://pages.github.com/) and uses [Hexo](https://hexo.io/) as blog engine.

For the setup I used the following resources:
- [Installation of Hexo on GitHub](http://jdpaton.github.io/2012/11/05/setup-hexo/)
    - *some commands are outdated, but the procedure becomes prette clear*
- [Full Installation Documentation by Digital Ocean](https://www.digitalocean.com/community/tutorials/how-to-create-a-blog-with-hexo-on-ubuntu-14-04)
- [Next-Theme](https://github.com/iissnan/hexo-theme-next)
- [MathJax-Fix with hexo-renderer-mathjax](https://nathaniel.blog/tutorials/make-hexo-support-math-again/)
    - *changing `<your-project-dir>/node_modules/hexo-renderer-kramed/lib/renderer.js` was not needed*
- ~~[MathJax-Fix with Hexo-Mat](https://typewind.github.io/2017/03/12/mathjax/)~~
    - Hexo-Mat did not work properly

Click *more* to see some initial playing-around with Hexo..

<!-- more --> 

# This is some beautiful math rendering

Simple inline $a_i = b_i + c_i$.


$$
\frac{\partial u}{\partial t}
= h^2 \left( \frac{\partial^2 u}{\partial x^2} +
\frac{\partial^2 u}{\partial y^2} +
\frac{\partial^2 u}{\partial z^2}\right)
$$

Let's try some function definitions

$$f(x) = 2x + 1$$

$$ p(x~|X) = \int_\theta p(x~|\theta,X)*p(\theta|X,a) $$

# This is some text-highlighting

*Temporary End...*
**Oh, I forgot!**

# Some referencing techniques

Blockquote...

{% blockquote [author[, source]] [link] [source_link_title] %}
content
{% endblockquote %}

Blockquote 2...

{% blockquote Seth Godin http://sethgodin.typepad.com/seths_blog/2009/07/welcome-to-island-marketing.html Welcome to Island Marketing %}
Every interaction is both precious and an opportunity to delight.
{% endblockquote %}


# Let`s try some links

[See here for more Details](/assets/test.html)
[Download file here](/assets/d3-3.5.5.min.js)

# Some code-highlighting

{% codeblock lang:objc %}
[rectangle setX: 10 y: 10 width: 20 height: 20];
{% endcodeblock %}

```javascript
var i = 1
while(i < 100){
    i++
}
```

# Let`s embed an image

![](/images/dummy1.jpg)

# Let`s make a table

| Tables        | Are           | Cool  |
| ------------- |:-------------:| -----:|
| col 3 is      | right-aligned | $1600 |
| col 2 is      | centered      |   $12 |
| zebra stripes | are neat      |    $1 |

# Let`s try something with plain HTML

{% raw %}
<script src="https://cdnjs.cloudflare.com/ajax/libs/d3/3.5.5/d3.min.js"></script>
<script src="https://wzrd.in/standalone/function-plot@1.18.1"></script>
<p><b> I am plain HTML</b></p>
<p>
<script> document.write("And I'm the Javascript-Plotter")</script>
</p>
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
Thanks to [Maricio Poppe](https://github.com/mauriciopoppe/function-plot)