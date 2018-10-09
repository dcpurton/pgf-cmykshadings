# pgf-cmykshadings — Support for CMYK shadings in PGF/TikZ

The `pgf-cmykshadings` package provides support for CMYK shadings in PGF/TikZ.

At present functional shadings are not supported.

It will only work with `pdflatex`, `lualatex`, and `xelatex`.

## Usage

Just add `\usepackage{pgf-cmykshadings}` to your document preamble.

### Colour models

By default, `pgf-cmykshadings` will always produce CMYK shadings unless the
current `xcolor` colour model is RGB, in which case an RGB shading will be
produced. This is equivalent to using the `cmyk` package option.

The package option `rgb` will always produce `rgb` shadings unless the current
`xcolor` colour model is CMYK, in which case a CMYK shading will be produced.

In practice this means that if you are using the natural colour model of `xcolor` you can still get mismatched colours if you, for example, create a shading from green (which is defined as RGB) to cyan (which is defined as CMYK). The shading has to pick one colour model and will look different to one of the solid colours.

It is recommended to always load `xcolor` before before `pgf-cmykshadings` with
either the `rgb` or `cmyk` option to avoid colour surprises.

### Load order

- `pgf-cmykshadings` should be loaded *before* any shadings are defined
  otherwise these will be defined as RGB. This means you should load
  `pgf-cmykshadings` before (for example) `tikz` and `beamer`.
- If you want to pass custom options to `xcolor` (e.g., a colour model or set
  of named colours), you should load `pgf-cmykshadings` *after* `xcolor` or use
  `\PassOptionsToPackage{...}{xcolor}` before loading `pgf-cmykshadings`.

### Explicitly choosing RGB or CMYK shadings

RGB shadings can always be set up using:

  - `\pgfdeclarehorizontalrgbshading`
  - `\pgfdeclareverticalrgbshading`
  - `\pgfdeclareradialrgbshading`

And then used with `\pgfusergbshading`.

Similarly, CMYK shadings can always be set up using:

  - `\pgfdeclarehorizontalcmykshading`
  - `\pgfdeclareverticalcmykshading`
  - `\pgfdeclareradialcmykshading`

And then used with `\pgfusecmykshading`.

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

