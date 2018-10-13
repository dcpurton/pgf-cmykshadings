# pgf-cmykshadings — Support for CMYK shadings in PGF/TikZ

The `pgf-cmykshadings` package provides support for CMYK shadings in PGF/TikZ.

It will only work with `pdflatex`, `lualatex`, and `xelatex`.

## Usage

Just add `\usepackage{pgf-cmykshadings}` to your document preamble.

### Colour models

`pgf-cmykshadings` tries to produce shadings consistent with the currently
selected `xcolor` colour model. `rgb`, `cmyk`, and `gray` are supported.

**Note:** The colour model chosen for a shading is the based on the `xcolor`
colour model *at the time the shading is created*. This is either when
`\pgfdeclare*shading` is called with no optional argument or when
`\pgfuseshading` is called if `\pgfdeclare*shading` was called with an optional
argument.

If the `xcolor` `natural` colour model is in use then the shading colour model
will be `cmyk` by default (equivalent to passing the `cmyk` option to the
`pgf-cmykshadings` package). `rgb` shadings can be output instead by passing
the `rgb` option to the `pgf-cmykshadings` package.

In practice this means that if you are using the `natural` colour model of
`xcolor` you can still get mismatched colours if you, for example, create a
shading from green (which is defined as RGB) to cyan (which is defined as
CMYK). The shading has to pick one colour model and will look different to one
of the solid colours.

It is recommended to always load `xcolor` before `pgf-cmykshadings` with either
the `rgb`, `cmyk`, or `gray` options to avoid colour surprises.

### Load order

- `pgf-cmykshadings` should be loaded *before* any shadings are defined
  otherwise these will be defined as RGB. This means you should load
  `pgf-cmykshadings` before (for example) `tikz` and `beamer`.
- If you want to pass custom options to `xcolor` (e.g., a colour model or set
  of named colours), you should load `pgf-cmykshadings` *after* `xcolor` or use
  `\PassOptionsToPackage{...}{xcolor}` before loading `pgf-cmykshadings`.

### General (functional) shadings

By nature, the PostScript® code used to generate functional shadings must
output either RGB or CMYK data. For this reason, `\pgfdeclarefunctionalshading`
is *not* portable across colour models.

Take particular care that the *same* colour model is in use at declaration time
and use time for functional shadings declared with an optional argument as
otherwise the PostScript® data will not match the declared colour space and you
will end up with a malformed PDF.

This also means that you should *not* use the functional shadings from the
`tikz` shading library (`bilinear interpolation`, `color wheel`, `color wheel
black center`, `color wheel white center`, and `Mandelbrot set`) except when
the `xcolor` RGB model is in use, otherwise you will end up with a malformed
PDF.

## Licence

```
Copyright (c) 2018 David Purton <dcpurton@marshwiggle.net>

This work may be distributed and/or modified under the conditions of
the LaTeX Project2 Public License, either version 1.3c of this license
or (at your option) any later version. The latest version of this
license is in
   http://www.latex-project.org/lppl.txt
and version 1.3c or later is part of all distributions of LaTeX
version 2005/12/01 or later.

This work is "maintained" (as per the LPPL maintenance status)
by David Purton.

This work consists of the file style file pgf-cmykshadings.sty and the
driver files:
  - pgfsys-cmykshadings-pdftex.def
  - pgfsys-cmykshadings-xetex.def
  - pgfsys-cmykshadings-luatex.def
  - pgfsys-cmykshadings-divpdfmx.def


All code in these files is taken from the PGF files pgfcoreshade.code.tex,
pgfsys-pdftex.def, pgfsys-dvipdfmx.def, and pgfsys-luatex.def
Copyright (c) 2006 Till Tantau and then slightly modified to output CMYK
gradients instead of RGB ones.
```

