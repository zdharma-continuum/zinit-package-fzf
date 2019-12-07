# junegunn/fzf as a Zsh package

##### NPM link: [https://www.npmjs.com/package/zsh-fzf](https://www.npmjs.com/package/zsh-fzf)

[Zplugin](https://github.com/zdharma/zplugin) can use the NPM package registry
to automatically:

- get the plugin's Git repository OR release-package URL,
- get the list of the recommended ices for the plugin,
    - there can be multiple lists of ices,
    - the ice lists are stored in *profiles*; there's at least one profile, *default*,
    - the ices can be selectively overriden.

Example invocations that'll install
[junegunn/fzf](https://github.com/junegunn/fzf) either from the release archive
or from Git repository:

```zsh
# Download the package with the default ice list
zplugin pack for fzf

# Download the package with the bin-gem-node annex-utilizing ice list
zplugin pack"bgn" for fzf

# Download with the bin-gem-node annex-utilizing ice list FROM GIT REPOSITORY
zplugin pack"bgn" git for fzf
```

## Default Profile

Provides the fuzzy finder via Makefile-installation of the `fzf` binary under
`$ZPFX/bin`.

```zsh
zplugin lucid as=program pick="$ZPFX/bin/(fzf|fzf-tmux)" \
    atclone="cp shell/completion.zsh _fzf_completion; cp bin/fzf-tmux $ZPFX/bin" \
    make="PREFIX=$ZPFX install" \
    …
```

## Bin-Gem-Node Profile

Provides the fuzzy finder via *shims*, i.e.: automatic forwarder scripts created
under `$ZPFX/bin` (which is added to the `$PATH` by default). It needs the
[bin-gem-node](https://github.com/zplugin/z-a-bin-gem-node) annex.

```zsh
zplugin lucid as=null make \
    atclone="cp shell/completion.zsh _fzf_completion" \
    sbin="fzf;bin/fzf-tmux" \
    …
```

<!-- vim:set ft=markdown tw=80 fo+=an1 autoindent: -->
