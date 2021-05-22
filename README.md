# zeno.zsh

zsh fuzzy completion and utility plugin with [Deno](https://deno.land/).

**WARNING**: This project is in beta stage and WIP README.

## Requirements

- [Deno](https://deno.land/)

### Install macOS

```sh
$ brew install deno
```

## Installation

### zinit

```zsh
zinit ice lucid depth"1" blockf
zinit light yuki-yano/zeno.zsh
```

### git clone

```sh
$ git clone https://github.com/yuki-yano/zeno.zsh.git
$ echo "source /path/to/dir/zeno.zsh" >> ~/.zshrc
```

## Usage

### Completion

```sh
$ git add <Tab>
Git Add Files> ...
```

### Abbrev snippet

Require [user configuration file](#user-configuration-file-example)

```sh
$ gs<Space>

Insert
$ git status --short --branch
```

```sh
$ gs<Enter>

Execute
$ git status --short --branch
```

### Insert snippet

Use zeno-insert-snippet zle

### Search history

Use zeno-history-completion zle

## Configuration example

### Completion and abbrev snippet

```zsh
# default
export ZENO_GIT_CAT="cat"
# git file preview with color
# export ZENO_GIT_CAT="bat --color=always"

# default
export ZENO_GIT_TREE="tree"
# git folder preview with color
# export ZENO_GIT_TREE="exa --tree"

bindkey ' '  zeno-auto-snippet
bindkey '^m' zeno-auto-snippet-and-accept-line
bindkey '^i' zeno-completion
```

### ZLE widget

```zsh
bindkey '^r'   zeno-history-selection
bindkey '^x^s' zeno-insert-snippet
```

## Builtin completion

- git
  - add
  - diff
  - diff file
  - checkout
  - checkout file
  - switch
  - reset
  - reset file
  - restore
  - fixup and squash commit
  - rebase
  - merge

See: https://github.com/yuki-yano/zeno.zsh/blob/main/src/completion/source/git.ts

## User configuration file example

```sh
$ touch ~/.config/zeno/config.yml
```

and

```yaml
snippets:
  # snippet and keyword abbrev
  - name: git status
    keyword: gs
    snippet: git status --short --branch
  # snippet with placeholder
  - name: git commit message
    keyword: gcim
    snippet: git commit -m '{{commit_message}}'

completions:
  - name: kill
    patterns: 
      - "^kill( -9)? $"
    sourceCommand: "ps -ef | sed 1d"
    options:
      --multi: true
      --prompt: "'Kill Process> '"
    callback: "awk '{print $2}'"
```