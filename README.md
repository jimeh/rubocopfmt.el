# rubocopfmt-mode

Emacs minor-mode to format Ruby code with [RuboCop][] on save via it's
`--auto-correct` option.

## Installing

Drop `rubocopfmt.el` somewhere into you `load-path` and require it. Personally I
favour the folder `~/.emacs.d/vendor`:

```lisp
(add-to-list 'load-path "~/.emacs.d/vendor")
(require 'rubocopfmt)
```

## Usage

To enable formatting `ruby-mode` buffers on save with rubocopfmt, simply enable
`rubocopfmt-mode` within `ruby-mode` with something like this in your config:

```lisp
(add-hook 'ruby-mode-hook #'rubocopfmt-mode)
```

## Commands

- `rubocopfmt` - Format current buffer with RuboCop.
- `rubocopfmt-mode` - Toggle formatting on save on/off.

[rubocop]: https://github.com/bbatsov/rubocop
[go-mode]: https://github.com/dominikh/go-mode.el
