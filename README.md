Building the slides
===================

Create a Python 3.4 environment with conda and install the hieroglyph package:

```
$ conda create -n py3lightning python=3.4
$ source activate py3lightning
$ conda install -c gmarkall hieroglyph
```

Build the slides:

```
$ make slides
```

View the slides with Firefox (or whatever browser):

```
$ firefox build/slides/index.html
```
