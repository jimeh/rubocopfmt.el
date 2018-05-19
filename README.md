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

## Commands

- `rubocopfmt` - Format current buffer with rubocopfmt.
- `rubocopfmt-mode` - Toggle formatting on save on/off.


[rubocopfmt]: https://github.com/jimeh/rubocopfmt
[go-mode]: https://github.com/dominikh/go-mode.el
