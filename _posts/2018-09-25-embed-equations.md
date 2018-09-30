---
layout: post
title: Embedding equations in GitHub blog posts with MathJax
tags: tools github-blog
excerpt: easiest way to embed equations in posts
mathjax: true
---

One of the first things I wanted to do for this blog was to be able to write equations as in LaTeX. I thought this would be straightforward, but it took some searching to find a better solution than embedding images of the equations generated by an external tool.
The simple answer is: use MathJax that has a syntax almost identical to LaTeX. More recent GitHub themes (I forked [Jekyll Now](https://github.com/barryclark/jekyll-now)) already have kramdown enabled in the *\_config.yml* file, supporting MathJax.  

The steps are then the following:  

1) If you want to use equations in your blog posts as I do, paste the following script into *post.html* that should be in your *layouts* folder

```
<script type="text/javascript" src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML"></script>
<script>
        MathJax.Hub.Config({
            config: ["MMLorHTML.js"],
            extensions: ["tex2jax.js","TeX/AMSmath.js","TeX/AMSsymbols.js"],
            jax: ["input/TeX"],
            tex2jax: {
                inlineMath: [ ['$','$'], ["\\(","\\)"] ],
                displayMath: [ ['$$','$$'], ["\\[","\\]"] ],
                processEscapes: false
            },
            TeX: {
                TagSide: "right",
                TagIndent: ".8em",
                MultLineWidth: "85%",
                equationNumbers: {
                   autoNumber: "AMS",
                },
                unicode: {
                   fonts: "STIXGeneral,'Arial Unicode MS'"
                }
            },
            showProcessingMessages: false
        });
</script>
```
**within the block**:  

\{ % if page.mathjax % \}  
\(code comes here\)  
\{ % endif % \}

This means that you can set up a *mathjax* flag for those posts where you'll have equations.  

2) In the posts where you'll have equations insert the flag  
**mathjax: true**

3) You can now write equations between double \$ signs such as

$$
    \begin{bmatrix} X_1\\ X_2\\ \end{bmatrix} = \begin{bmatrix} a_{11} & a_{12}\\ 0 & 0\\ \end{bmatrix}
    \begin{bmatrix} X_1\\ X_2\\ \end{bmatrix} + \begin{bmatrix} 0\\ h_2\\ \end{bmatrix}
    \begin{bmatrix} l_1 & l_2 \end{bmatrix} \begin{bmatrix} X_1\\ X_2\\ \end{bmatrix}
    + \begin{bmatrix} da\\ dh + C_k \end{bmatrix}  
$$

A good resource for different formulae [is here](https://math.meta.stackexchange.com/questions/5020/mathjax-basic-tutorial-and-quick-reference).