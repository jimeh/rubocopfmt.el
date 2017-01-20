# rubocopfmt-mode

Emacs minor-mode to format Ruby code with [rubocopfmt][] on save.

Core parts of `rubocopfmt-mode` are borrowed from [`go-mode`][go-mode] and it's
invocation of `gofmt`.

## Installing

Install [rubocopfmt][]:

```
gem install rubocopfmt --pre
```

Drop `rubocopfmt.el` somewhere into you `load-path`. I favour the folder
`~/.emacs.d/vendor`:

```lisp
(add-to-list 'load-path "~/.emacs.d/vendor")
(require 'rubocopfmt)
```

## Usage

To enable formatting `ruby-mode` buffers with rubocopfmt on save, simply enable
`rubocop-mode` within `ruby-mode` with something like this in your config:

```lisp
(add-hook 'ruby-mode-hook #'rubocopfmt-mode)
```

You can also toggle `rubocopfmt-mode` on/off with `M-x rubocopfmt-mode`.

## License

Copyright (C) 2017 Jim Myhrberg

Permission is hereby granted, free of charge, to any person obtaining a copy of
this software and associated documentation files (the "Software"), to deal in
the Software without restriction, including without limitation the rights to
use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of
the Software, and to permit persons to whom the Software is furnished to do so,
subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS
FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR
COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER
IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN
CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.


[rubocopfmt]: https://github.com/jimeh/rubocopfmt
[go-mode]: https://github.com/dominikh/go-mode.el
