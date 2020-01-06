----
title: Trying out Observable
----

[Observable][observable] is a web app for making interactive notebooks. I've
been interested in the idea since I heard of it, and recently I decided to try
it out by porting [one of my Jupyter notebook posts][mynotebook] to Observable.

[observable]: https://beta.observablehq.com/
[mynotebook]: https://github.com/luanthe/notebooks/blob/master/2018-06-28%20continued%20rational%20function%20approximations.ipynb

First order of business was figuring out how to make a simple line plot. I'm not
aware of a Javascript analogue of Python `matplotlib` that is widely used. I
know there's [D3][d3], but my impression is that D3 is more designed for
building custom fancy interactive visualizations, and it seemed too big and
complicated when basically all I want to do is `plot(x, y)`.

Through looking at some Observable example notebooks I came across
[Vega-Lite][vegalite], which seemed a bit simpler to use. It's still fancier
than `matplotlib`; my Python code for the first plot

[d3]: https://d3js.org/
[vegalite]: https://vega.github.io/vega-lite/

```
x = np.linspace(-0.5, 0.5)
y = np.log1p(x)

plt.plot(x, y)
plt.axhline(0, color='black')
plt.axvline(0, color='black')
```

became a 15+ line JSON description of how to render the plot.

I mean, okay, this is fine. Vega-Lite is (I think?) designed for web documents
that are rendered over and over again, so it makes sense that it makes you
specify plots using a more explicit, declarative style. And at least I can put
most of the plot options into a function that I can reuse throughout a notebook.
