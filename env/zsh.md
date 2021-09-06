# Zsh

{% embed url="https://github.com/zsh-users/antigen" caption="Lightweight package manager for zsh " %}

The actual process for changing your default shell from Bash to ZSH is extremely easy. Just run `chsh -s /bin/zsh`.

> _**Note**_ that you'll need to supply the correct path your ZSH binary which you can get with the `which zsh` command we used earlier. [Click here](https://linux.die.net/man/1/chsh) for more information on the `chsh` command.

#### Example antigen.zsh

```text
source $HOME/antigen.zsh

# Load the oh-my-zsh's library.
antigen use oh-my-zsh

# Bundles from the default repo (robbyrussell's oh-my-zsh).
antigen bundle git
antigen bundle heroku
antigen bundle pip
antigen bundle docker
antigen bundle kubernetes
antigen bundle lein
antigen bundle fzf
antigen bundle gatsby
antigen bundle httpie
antigen bundle mosh
antigen bundle yarn
antigen bundle alias-finder
antigen bundle command-not-found
antigen bundle marlonrichert/zsh-autocomplete
antigen bundle zsh-users/zsh-syntax-highlighting
antigen bundle Sparragus/zsh-auto-nvm-use

# Syntax highlighting bundle.
antigen bundle zsh-users/zsh-syntax-highlighting

# Load the theme.
antigen theme robbyrussell
```

