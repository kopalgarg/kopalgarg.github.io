---
layout: post
title: Adding LaTeX formulas in GitHub markdown
published: true
---

GitHub markdown doesn't support inline formulas, so it isn't possible to write something like this in LaTeX `$\omega=d\phi/dt$`. A possible workaround to this issue is as follows:

Write your formula as you normally would in LaTeX and use this [tool](https://www.codecogs.com/latex/eqneditor.php) to convert it to an .png.

Copy the image address and insert it as an image using `<img src="">`. 
This will look something like this <img src="https://render.githubusercontent.com/render/math?math=\omega=d\phi/dt">.

Another workaround is to add the following code to markdown files:

```
<script type="text/javascript" async
  src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.0/MathJax.js?config=TeX-MML-AM_CHTML">
</script>
<script type="text/x-mathjax-config">
  MathJax.Hub.Config({
    tex2jax: {inlineMath: [['$','$'], ['\\(','\\)']]}
  });
</script>
```
