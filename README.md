# rubocopfmt.el

Emacs minor-mode to format Ruby code with
[RuboCop](https://github.com/bbatsov/rubocop) on save via it's `--auto-correct`
option.

## Installation

Drop `rubocopfmt.el` somewhere into you `load-path` and require it. Personally I
favour the folder `~/.emacs.d/vendor`:

```lisp
(add-to-list 'load-path "~/.emacs.d/vendor")
(require 'rubocopfmt)
```

## Usage

To enable formatting `ruby-mode` buffers on save, simply enable
`rubocopfmt-mode` with something like this in your config:

```lisp
(add-hook 'ruby-mode-hook #'rubocopfmt-mode)
```

## Commands

- `rubocopfmt` - Format current buffer with RuboCop.
- `rubocopfmt-mode` - Toggle formatting on save on/off.

## Internals

`rubocopfmt` works by executing `rubocop` against the file you are saving. To
ensure RuboCop behaves as expected, it is executed from within the same
directory as the file you are saving.

## Bundler Integration

If a `Gemfile` is found in the current directory or in any parent directory,
`bundle exec rubocop [...]` will be used to execute RuboCop. This does mean that
projects with a `Gemfile` are required to have `rubocop` listed as a dependency
for rubocopfmt to work.

This ensures that formatting is done with the same version of RuboCop that the
project lists as a dependency.

If you don't care about having a specific version of RuboCop and/or are using it as an
external tool, but still use a `Gemfile`, you can opt out from this behaviour by configuring
the option `(setq rubocopfmt-use-bundler-when-possible nil)`.

## Disabled Cops

There's a few of cops in RuboCop that can cause confusion and annoyance when run
against work-in-progress code. Hence `rubocopfmt` disables the worst offenders
by default. You can configure which cops are disabled by customizing the
`rubocopfmt-disabled-cops` variable.

Cops disabled by default:

- `Lint/Debugger`: Removes `debugger` statements. Not helpful when you need to
  debug something.
- `Lint/UnusedBlockArgument`: Don't prefix unused block argument variable names
  with `_`. This cop causes issues if you save after defining a block, but
  before you use all arguments of the block.
- `Lint/UnusedMethodArgument`: Don't prefix unused method argument variable
  names with `_`. This cop causes issues if you save after defining a method,
  but before you use all arguments of the method.
- `Style/EmptyMethod`: Don't remove remove empty line for empty methods. This
  cop is annoying if you save right after defining a new method.
