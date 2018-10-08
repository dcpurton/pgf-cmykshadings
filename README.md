# pgf-cmykshadings — Support for CMYK shadings in PGF/TikZ

The `pgf-cmykshadings` package provides support for CMYK shadings in PGF/TikZ.

At present functional shadings are not supported.

It will only work with `pdflatex`, `lualatex`, and `xelatex`.

## Usage

Just add `\usepackage{pgf-cmykshadings}` to your document preamble. CMYK
shadings are used by default.

RGB shadings can continue to be used by using the following macros:

  - `\pgfdeclarehorizontalrgbshading`
  - `\pgfdeclareverticalrgbshading`
  - `\pgfdeclareradialrgbshading`

An RGB shading can then be used with `\pgfusergbshading`.

It is also possible to retain RGB shadings as the default and use CMYK shadings
on demand. This can be set up by loading `pgf-cmykshadings` with the
`nodefault` option. In this case, CMYK shadings can be set up using the
following macros:

  - `\pgfdeclarehorizontalcmykshading`
  - `\pgfdeclareverticalcmykshading`
  - `\pgfdeclareradialcmykshading`

And a CMYK shading can then be used with `\pgfusecmykshading`.

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

