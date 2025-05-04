# Markdown

## KaTeX

**Note:** GitHub supports [MathJax](https://github.blog/changelog/2022-05-19-render-mathematical-expressions-in-markdown/) and not KaTex, so KaTeX is not displayed properly on GitHub. However, it has been displayed properly in the Jupyter Notebooks that I have tried.

### Inline  rendering:

`$`

```
$ f_{\mathbf{w},b}(\mathbf{x}^{(i)}) = \mathbf{w} \cdot  \mathbf{x}^{(i)} + b $, to predict $y$ given $x$.
```
outputs this:

$ f_{\mathbf{w},b}(\mathbf{x}^{(i)}) = \mathbf{w} \cdot  \mathbf{x}^{(i)} + b $, to predict $y$ given $x$.

### Block rendering:

`$$`

If you use `$$`, you need to start and end the line with them, like this:

```
$$ f_{\mathbf{w},b}(\mathbf{x}^{(i)}) = \mathbf{w} \cdot  \mathbf{x}^{(i)} + b $$
, to predict $y$ given $x$.
```

$$ f_{\mathbf{w},b}(\mathbf{x}^{(i)}) = \mathbf{w} \cdot  \mathbf{x}^{(i)} + b $$
, to predict $y$ given $x$.


Some functions only work with block rendering, e.g. `\tag`:

```
$$g(z) = \frac{1}{1+e^{-z}}\tag{1}$$
```
outputs:

$$g(z) = \frac{1}{1+e^{-z}}\tag{1}$$
