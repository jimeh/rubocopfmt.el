# rubocopfmt.el

Emacs minor-mode to format Ruby code with
[RuboCop](https://github.com/bbatsov/rubocop) on save via it's `--auto-correct`
option.

## Installation

Available on MELPA as [`rubocopfmt`](https://melpa.org/#/rubocopfmt).

### use-package

```elisp
(use-package rubocopfmt
  :hook
  (ruby-mode . rubocopfmt-mode))
```

### package.el

```
M-x package-install rubocopfmt
```

Then add the following to your Emacs config:

```elisp
(require 'rubocopfmt)
(add-hook 'ruby-mode-hook #'rubocopfmt-mode)
```

### Manual

Place `rubocopfmt.el` somewhere into you `load-path` and require it. For example
`~/.emacs.d/vendor`:

```elisp
(add-to-list 'load-path "~/.emacs.d/vendor")
(require 'rubocopfmt)
(add-hook 'ruby-mode-hook #'rubocopfmt-mode)
```

## Usage

With `rubocopfmt-mode` enabled, Ruby buffer will automatically be formatted with
RuboCop on save.

## Commands

- `rubocopfmt` - Format current buffer with RuboCop.
- `rubocopfmt-mode` - Toggle automatic formatting on save on/off.

## Internals

`rubocopfmt` works by executing `rubocop` against the file you are saving. To
ensure RuboCop behaves as expected, it is executed from within the same
directory as the file you are working on.

## Bundler Integration

If a `Gemfile` is found in the current directory or in any parent directory,
`bundle exec rubocop [...]` will be used to execute RuboCop. This does mean that
projects with a `Gemfile` are required to have `rubocop` listed as a dependency
for rubocopfmt to work.

This ensures that formatting is done with the same version of RuboCop that the
project lists as a dependency.

If you don't care about having a specific version of RuboCop and/or are using it
as an external tool, but still use a `Gemfile`, you can opt out from this
behaviour by setting `rubocopfmt-use-bundler-when-possible` to `nil`.

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

## Performance

RuboCop is not very fast, often taking as much as 1-3 seconds to run. This can
be annoying, but there's a couple of options to improve performance. Both seem
to get the formatting time down to around 100-200ms just.

### rubocop-daemon

With [rubocop-daemon](https://github.com/fohte/rubocop-daemon) you end up with a
rubocop server running in the background. If you try this out, I highly
recommend using the bash script wrapper they provide, as that yields the best
possible performance.

### lsp-mode / solargraph

If you use [lsp-mode](https://github.com/emacs-lsp/lsp-mode) and
[solargraph](https://github.com/castwide/solargraph), with it configured to use
RuboCop as a reporter, then `lsp-format-buffer` should be able to format Ruby
buffers extremely fast.

`rubocopfmt-mode` can use `lsp-format-buffer` instead of `rubocopfmt` to format
buffers on save. This is currently an experimental feature, but you can turn it
on by customizing `rubocopfmt-on-save-use-lsp-format-buffer` and setting it to
`t`.
